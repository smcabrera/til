# Scopes and SQL for rails

Thursday, April 16th, 2015

A couple things that I just learned from this last refactoring (sha: 785fd760cd3bb02c39d05dbb7325b8719d4214cd for blocipedia project)

1. Scopes are good. Learn how to use those to avoid either having way too much logic in the controller layer, and/or creating unnecessary controller actions (both of which I've done). It's also a good way to avoid duplicating knowledge across your application, as well as making it clearer by giving things names. A long series of conditionals is much less readily understandable than a ```visible_to_premium_users``` scope.
2. Sometimes plain 'ol SQL is better. I think at the point where you've created an array and are adding to it instead of just reaching for an ```OR``` in SQL, you're probably better off looking at writing an SQL query to do the same thing. Just remember to always sanitize your SQL to avoid injection.
