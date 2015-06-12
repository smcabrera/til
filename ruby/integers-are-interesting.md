# Integers are Interesting

So I was playing around creating a little library for dealing with Peruvian visas and as I was debugging something I found that something which I had coerced to an integer was displayed as a Fixnum when I asked it what it's class was. Check out the following code:

```ruby
pry> "7".to_i.class
=> Fixnum
```

I thought ```to_i``` meant "to integer" but then it made it a Fixnum instead! What's going on?

So of course I googled "What's the difference between Integer and Fixnum". This was the winning result:



