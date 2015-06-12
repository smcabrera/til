# 404 Errors in Sources
This is something that has happened to me twice now so I figured it's time that I make a note of it. If you're using ubuntu all sorts of weird problems can come up from seemingly unrelated places when the command
```
sudo apt-get update
```
fails. This is the command that is updating all the software you've installed from the ubuntu repositories to the latest versions. Of course sometimes software gets deleted or discontinued and is no longer in the repositories. If for some reason it's in your sources list then you'll get 404 errors.

Also [this](http://askubuntu.com/a/92897/363205) stack overflow answer is incredibly useful.

(I realize the above explanation is a little incomplete--need to flesh it out more at some point)
