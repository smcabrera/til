# Splat Operator
At least, I think that's what this is--unless I'm confusing this with something else. Basically I just wanted to make a note that you're allowed to do stuff like this:

```
array = [1, 2, 3]
element, *rest
element
=> 1
rest
=> [2, 3]
```
Still not totally sure how this works so this is also a reminder to myself to go look this up when I have internet.

```ruby
def sum *numbers
  numbers.inject{ |sum, number| sum += number }
end

# sum 1, 2, 3
# => 6
```

And what if you want to pass in an array? I just had this come up and I got the scoop from this stack overflow answer. You just pass in an asterisk (splatting it again!)

```shell
$ arr = [1, 2, 3]
$ sum *arr
=> 6
```

