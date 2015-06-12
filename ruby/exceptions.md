# Exceptions

Notes from after my meeting with Michael on Thursday, April 23rd, 2015

I just finished an attempt at a user flow where users can update their account by signing up for a subscription plan through stripe. Everything was going well but for some reason my controller wasn't finishing. It never reached the end of the if branches where rendering was supposed to happen so it kept asking me to render a create.html.erb file. Totally weird.

This is the original file

https://gist.github.com/smcabrera/a320652743184cb8abea

The problem here was the rescue block that I inherited from the tutorial I'd stolen the stripe integration code from. This revealed to my ignorance on the subject of exceptions in ruby (or in any language actually!) so I decided that it's something I need to look into more.

A couple things based upon our discussion

1. Here's how rescue works generally
My code editor was telling me "no" when I tried to just put a rescue block all by itself like this

```ruby
rescue Stripe::CardError => e
  redirect_to edit_user_registration_path
  flash[:error] = e.message
end
```
I didn't even really try the above for long because it set off my linters (courtesy of the vim plugin syntastic). Reproducing the code by itself my linter will give me the following errors:

```
   unexpected keyword_end, expecting end-of-input
```
and
```
   unexpected keyword_rescue
```

So what's going on here?

Well apparently I should have looked into this more. ```rescue```  isn't a keyword that starts it's own block but it is a part of another block. Sort of like ```elsif``` and ```else``` as part of ```if``` or ```unless``` blocks. They should look something more like this:

```ruby
begin
  puts "Do some stuff"
rescue Stripe::CardError => e
  puts "Do stuff when this error happens"
rescue
  "Catch-all error I don't know how to identify"
end
```

This sounds really useful, especially when you're using external services like Stripe where you know they might fail for reasons beyond your control.

That last bit is something else that Michael mentioned that I wanted to take note of. You basically catch these different categories of errors and then you say what you're going to do in each error case. If you don't supply anything to rescue then you're just using it as a catch-all for errors that you don't know what to do with. This initially sounded like a great idea to me, but Michael explained that really it's kind of a smell. If you feel the need to include a rescue for errors that you don't know about...you should probably work on identifying what kind of errors are likely to occur. In the case of the Stripe::CardError this is an error class supplied to us by stripe and this is a thing that we know is going to happen sometimes. Credit cards fail to get processed sometimes and it's not the code's fault. Part of the purpose of exceptions is to deal with stuff that you know could go wrong. Ideally you should really plan for all of them and deal with them accordingly.

Anyway...clearly this is a topic I need to investigate more. Which brings me to...

2. *Exceptional Ruby:* Avdi Grimm has a great book on the subject called Exceptional Ruby. I'd heard of the book before but now I feel more motivated to check it out. Also Michael said he'd buy me a copy--awesome!

