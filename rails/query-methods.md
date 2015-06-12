# Active Record Query Methods
There's a lot more rails query methods than the ones I tend to use on a regular basis. It might be a good idea to just pull out the list and start playing around with them every now and then to get a feel for when each one would be useful. For example when I'm playing around with my models in the rails console, I'll generally do something like this:

```
u = User.first
u.posts
```

To grab a user and check out his posts. I don't really care that it's the first user. It's just the quickest way that comes to mind to grab a user since I don't care about querying for a particular user. Since it doesn't need to be the first user, I could have instead done this

```
u = User.take
u.posts
```

This just gives me a user in no particular order. It's equivalente to the SQL:

```
SELECT * FROM clients LIMIT 1
```
as opposed to the slightly longer
```
SELECT * FROM clients ORDER BY clients.id ASC LIMIT 1
```
of using first.

Why does this matter? Well, it doesn't particularly. I suppose as a habit I'd be better off using take when I don't need it to be first because it's a little faster. But I'm just playing around in the database so performance isn't a big issue. No I think rather it's good if I'm going to be making queries on the database anyway that I take advantage of the opportunity to learn something. Try out methods I hadn't heard of before and compare them to the ones I typically use. I think getting familiar with the methods available and getting used to looking up what you need quickly is going to be advantageous in the long run because you'll immediately go straight to the method you need when the situation arises.

This is all from the rails guides; I'm not reinventing the wheel here. The complete list of query methods and what they do is available [here](http://guides.rubyonrails.org/active_record_querying.html)

At the bottom I've got the full list as a reference. I intend to come back and revise these periodically and see what I can learn. But there's actually a shortcut to going to the rails guides and looking at the whole list. These are all methods on the class ActiveRecord::QueryMethods

So now we know where they live we can look them up whenever we're in the rails console as long as we're using pry (I always am).

```
cd ActiveRecord::QueryMethods
ls
```

and BAM! You've got the complete list of query methods

## Complete list of query methods
bind
create_with
distinct
eager_load
extending
from
group
having
includes
joins
limit
lock
none
offset
order
preload
readonly
references
reorder
reverse_order
select
uniq
where



