# Receive Matcher
I'm not planning to make a note of every rspec matcher but I wanted to point out this one that wasn't obvious to me and I wouldn't have looked it up on my own. So if you want to know if some object is "capable" of some action (if it's allowed to receive a message you can do something like this)

```
  expect( SomeClass ).not_to receive(:some_message)
```

Hold on though. What do we mean by message? This is not something I was completely familiar with. I'd heard it thrown around before but I still wasn't totally clear on what it meant. What do we mean exactly when we say "message". Is that just a synonym for "argument"? Or method call?

I did some investigating. Apparently back when the term Object Oriented Programming was first coined for SmallTalk it came along with the idea of objects sending and receiving messages from each other. In fact, the creator of SmallTalk later said that he regretted the object idea having been picked up over the idea of messages, which he thought was actually the stronger idea.

See [this](http://stackoverflow.com/a/15593153/2181217) answer on stack overflow where I figured that out from, while [this](http://c2.com/cgi/wiki?AlanKayOnMessaging) is the article where Alan Kay, creator of SmallTalk, discusses this.

Okay, fine but getting down to hard tacks what does this actually mean in practice for my understanding of OOP in ruby?

I cooked up an example to explain this to myself that hopefully others find useful.

Here's two objects that need to communicate to each other, a dog and its master. The master wants to tell the dog what to do, like speak, sit or roll over. Let's build some classes to represent this:

```
class Dog
  attr_accessor :name

  def initialize(name)
    @name = name
  end

  def speak
    puts 'woof'
  end
end

class Master
  def command_dog_to_speak(dog)
    dog.speak
  end

  def tell_me_your_name(dog)
    dog.name
  end
end
```
So now we've got some classes, let's instantiate these in objects:

```
spot = Dog.new("spot")
steve = Master.new
```

So with this now I have a master, steve, who can tell the dog to do a few things. He can tell the dog "speak" like this:

```
steve.command_dog_to_speak(spot)
woof
=> nil
```
I issue my command, pass in an instance of the Dog class and I get my dog to bark.

So in this case the spot object is receiving the message speak from the steve object.

```
spot.respond_to?(:speak) # => true
spot.respond_to?(:roll_over) # => false
```

Returns false because this dog doesn't know how to roll over

```
steve.tell_me_your_name(spot)
spot.respond_to?(:name) #=> true
```

This will also return true because we've automatically created getter methods for name in the Dog class with the attr_accessor :name 

Even though we haven't explicitly defined a method, it's there implicitly with the attr_accessor

Even the name of the respond_to? method contains the language of sending and receiving messages

Also at some point check out [this article](https://robots.thoughtbot.com/back-to-basics-polymorphism-and-ruby) from thoughtbot about polymorphism.




