# Has Many Through Relationship and learning through high level discussions

Thursday April, 16th, 2015

Today with Michael we went over the has many through relationship in rails. I thought he did a really good job explaining it and helping me discover what was going on as we walked through it together.

I'm going to come back here to write up a more thorough description of what's at play here, but for now I'll just put up a link to the spreadsheet: https://docs.google.com/spreadsheets/d/1d9NHzj5k0epfRU9XcLlRc7A4jmb-n2TOGbRDxHcJWnI/edit?usp=sharing

Also in general I'd like to point out what a super helpful thing a simple spreadsheet table can be for this purpose. For the sake of visualizing things it can be really helpful to go through and.

Also in this meeting I discovered that it can sometimes be more helpful to take a high level look at where to take things than to take the time to actually write code together. I often find that the biggest sticking points for me are when I'm disoriented and don't know quite where to start. In this sense just taking a look at existing code and talking about it in a high level way (what controller actions am I going to want, what model objects will I need to create, things like this) can be super helpful.

This *database playground* spreadsheet was the same kind of thing with thinking about modeling the database--we didn't touch the codebase at all, but I left with a really thorough understanding of what I needed to do to implement the kind of model relationships that I needed to and a a much deeper understanding of what was going on behind the scenes with the methods I needed to include in my models to get this to work.

## Subscriptions
Something I also want to write about as well as implement is how I intend to implement subscriptions for the blocipedia project. Right now the app is only set up to make one-time payments through stripe but a real SaaS app needs to have recurring payments through subscriptions.

We talked a bit about how this could be done. This is from my notes, but I hope to do a more complete write-up soon:

Stripe gives us back a customer id once it's done and it is this, along with our API key that is needed to make these charges.

So if we wanted to make ongoing charges we'd need to write this to the database so that we could use it again.

So then, instead of a one-time charge being triggered by the button, the button would trigger the ```create``` action of a ```SubscriptionController``` to create a new subscription. This subscription would have a subscription_date (so that the customer is billed on the same date every month--it wouldn't make sense to get billed on the 30th if you started on the 29th) and the customer id, both stored in the database for the Subscription object (so I'll need a model as well right?). Then the charge, instead of happening in the controller, would take place in a rake task, which we could set to be called every month via a cron job (check out the blocitoff app for an explanation of how to set this up--there are some tools that make it easier).

That rake task can then be set to trigger on the subscription date each month (30 days after the date every month or whatever).

The downgrade action then is simply a destroy action on the Subscription controller--it nukes the subscription and thus gets rid of the the subscription date (so that the client is no longer billed) and the customer id (so that the client can't be billed--never hurts to be safe). That same action should probably also be in charge of changing the user's role from premium to free. And, whether in the same action or elsewhere--it should trigger the changing of the client's associated wikis from private to public, and should also somehow tell the user that these things are happening (and possibly give them the option to delete wikis instead of letting them become public).

I'm not sure if that should all happen in the same method (it sounds like that would make for a very large method!) but it does seem clear that all these things do need to happen. Perhaps we put them all in the one method for now and we make a note to think about how you might extract those out and put them other places.









