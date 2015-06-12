# Duck Typing and Case Statements

Duck typing refers to when your program allows different kinds of objects (objects with different classes) and simply allows them to do different things based on what their class is. You don't prohibit arguments being passed in based on a specific class you just call it and then assume that the object has a way to respond to a certain method. Called "duck typing" based on the saying "if it looks like a duck and it quacks like a duck; it's a duck."

What if you need to actually check the types with a case statement? This article is helpful for that as it can be a little confusing.

http://stackoverflow.com/questions/3908380/ruby-class-types-and-case-statements

Also here's my example code from what I've been working on for whenever I decide to write this up:


Let's say I want to allow my initializer for a class to take different types as an input and then convert them into a date. I could have something like this:

```ruby
class PeruvianVisa
  def initialize(entry_date, days_granted = 90)
    self.entry_date = self.parse_date(entry_date)
    self.days_granted = days_granted
  end

  def parse_date(date)
    case date
    when Date
      date
    when Time
      date.to_date
    when String
      Chronic.parse(date).to_date
    else
      "Something else"
    end
  end
end
```
here I'm calling the parse_date method on the argument to new before saving it away as a part of the object's date, because I want to make sure that it's saved as a Date object for the other methods I'm going to define on this class. In order to be able to receive different kinds of arguments other than Date I have a case statement in the parse_date method switch on the class of the argument and then return the argument converted into a date.

Now that I think about it, I think the above isn't actually an example of duck typing...not yet.

I think (and it would be good to double check this) that duck_typing would be to say "hey, we can actually forget about the type checking and just assume that whatever gets passed in is something that has a to_date method and then just call its to_date method assuming that all the possible arguments will know how to turn themselves into dates.

Then the only one that would have to be checked for is String since strings are only able to be turned into dates when used we use the  Chronic library to do so.
