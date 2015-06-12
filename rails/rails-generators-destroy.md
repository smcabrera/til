# Reversing rails generators

I just learned this handy tip. Rather than going in and editing or deleting a generator that you miswrote somehow, you can reverse a rails generator--deleting all the files it created--just by using the destroy command instead of generate:

```
rails destroy controller ControllerName
```

This is way faster than going in and editing all the files you just created (this happened to me when I failed to make a controller name plural)
