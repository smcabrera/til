# How to setup a private git server
I'm taking this mostly from this digital ocean tutorial. Digital ocean tends to put out really good tutorials for doing server stuff on their blog. They really make an effort to make sure that their tutorials are up to date and specify the exact version of linux they're using for instance so the tutorial you're using is always going to match up precisely.

Even though I'm going through a tutorial I still find it useful to explain stuff to myself as I go through it so I can make sure I understand what I'm doing.

## Create the git user
So whenever you're pushing to a git remote the user you're accessing with ssh is git; that's why you always see git@ from github for instance. There's no magic here, you're just using ssh and ssh requires a username and an address. So let's start by making that address.

the tutorial says to run
```
su -
```
to enter as the superuser. Well that didn't work for me. But the point is that for starters you need to switch to the superuser, the user who is in charge of creating new users. For me that looked like this:
```
sudo su
```

Then to add the user it's just
```
useradd git
```

and to give him a password
```
passwd git
```

Now just for fun I'm going to doing all this through ansible. The advantage here is that once you get what's going on it's going to be much faster to replicate what you're doing because you have a proven recipe that you know works. All you have to do is change the variables around and you're good to go. I can't introduce everything to do with ansible right here, except to say that Servers for Hackers has the best most complete introduction that I've seen and the ansible documentation itself is great and that ansible in general is really friendly in general. As I go I'll just include the corresponding ansible instructions that will automate what I'm doing.

```

---
- name: Create a git user
  user: name=git password={{ password }}

```
Just add the above to the beginning of a tasks/main.yml file. In reality I'm realizing as I do this that this could probably just as easily be a single playbook file. Yeah, actually, let's just do that. Here's a playbook called staging-server.yml

```

---
- hosts: servername
  vars:
    - password: mypassword
  tasks:
  - name: Create a git user
    user: name=git password={{ password }}
```

All pretty straightforward--you define the hosts up top next to hosts. This is the name of the hosts group that you should have specified in a hosts.yml file.

Next vars is for variables that you're going to have access to throughout the playbook. For now let's just use this to put in the password. That way if you need to use that password throughout the playbook you've just got it defined up top and can change it in one place.

Finally there"s our first task which is setting up the git user. All ansible tasks either require you to specify command and include the shell bash  you need to run or else use some pre-specified modules. Here we use a built in module called "user". It takes a name and password and ensures that there's a user with that name and password. It'll create the user if it doesn't exist and if it does exist it'll just tell you so. Check out the [user module documentation](http://docs.ansible.com/user_module.html) for additional options like assigning the user to groups, making the user expire and similar fancypants options.

## Adding our ssh key to the access list
Now we need to give our git user our public key. First we'll want to create an ssh folder. For this we can create a task with the [file module](http://docs.ansible.com/file_module.html):

```
  - name: Create an ssh folder for the git user
    file: path=/home/git/.ssh state=directory
```

Then we need to actually put our public key up there. Turns out there's a [module for adding authorized keys](http://docs.ansible.com/authorized_key_module.html) too! We have several options here including grabbing the file from somewhere in the filesystem of the machine running the playbook. Or we could just grab them from github. See the examples in the docs for the module. I'm gonna try the github route.

```
  - name: Add our public key from github
    authorized_key: user={{ username }} key=https://github.com/{{ username }}.keys
```

Failing that I'll just add the file here and add it that way but that seems like more of a pain.





