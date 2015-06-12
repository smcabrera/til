
If you're just getting used to using active record query methods it can be a useful exercise to play around with those methods in the console to see what you get, and study the SQL that these methods produce to get a sense for that also. For instance I did this:

```shell
Wiki.all.where(:private => true, :user_id => 1).count
(8.9ms)  SELECT COUNT(*) FROM "wikis"  WHERE "wikis"."private" = 't' AND "wikis"."user_id" = 1
=> 0
```

I was then curious if I actually need that ```all``` method in there. Rather than mucking around in documentation, I just ran it without the ```all``` to see what happened.

```shell
»  Wiki.where(:private => true, :user_id => 1).count
(5.8ms)  SELECT COUNT(*) FROM "wikis"  WHERE "wikis"."private" = 't' AND "wikis"."user_id" = 1
=> 0
```

Sure enough the SQL is *exactly* the same, so it couldn't have been necessary in this case.

I think seeing that output was helpful for me figuring this out and in general, I think this is a great way to get a feel both for active record as well as for getting a handle on SQL if you're not already familiar with it.


