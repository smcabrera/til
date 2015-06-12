# Inject
I've known about inject before, but for some reason it's always confused me. I found some decent examples.

```
def smallest(array)
  array.inject do |accumulator, element|
    if element < accumulator
      element
    else
      accumulator
    end
  end
end
```
You pass inject two block arguments and one optional argument, which is the default or the start of the iteration

