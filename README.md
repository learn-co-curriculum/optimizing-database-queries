## Optimizing database queries

One part of the stack where we can think about improving our performance is with databases, and how we structure out database queries. 

### Use the database

We'll get to database tips in a minute, but the ultimate database performance tips, is to lean on the database as much as possible.  Databases are still very good at what they do, and therefore we should use them.  That is, instead of using a ruby method to select the proper data, or sum the proper data, lean on either activerecord or a raw sql query to perform the job.  

### N + 1 problem

The N + 1 problem occurs when we select a collection of rows from a table, and then for each row we make a separate query from the table.  For example, consider the following: 

```ruby 
	blogposts = BlogPost.all
	 
	blogposts.each do |blogpost|
	  blogpost.author.name
	end
```
If you consider what happens in the code above, activerecord first selects all of the blogposts.  And then for each blog post, it makes another query to the database to find the related author.  So how many queries are made overall - well one query for each blogpost, plus that initial query for all of the blogposts.  Thus, n + 1 queries, where n is the number of blogposts.  

Take a look at how to solve the n + 1 problem by watching the following railscast, or by referencing the RailsGuide below: 

* [RailsGuide on Eager Loading](http://guides.rubyonrails.org/active_record_querying.html#eager-loading-associations)
* [RailsCast on Eager Loading](http://railscasts.com/episodes/22-eager-loading-revised)

### Indexing

Databases are very good at scanning through lots of data quickly.  However, in a production database that can be a lot of information.  So a simple request to find whether a user by email (say, when authenticating a user) may become a costly request in production.

To solve this problem, you can add an index to a given column in a table.  Indexing works similar to how the hash data structure works, and we encourage you to review that lesson in the algorithm coursework if you need more information.

For more information, please view the following sources: 

* [Railscast on postgres Performance](https://www.youtube.com/watch?v=n41F29Qln5E)
* [Blogpost on Indexing](http://www.rakeroutes.com/blog/increase-rails-performance-with-database-indexes/)
* [What to Index - StackOverflow](https://stackoverflow.com/questions/3658859/when-to-add-what-indexes-in-a-table-in-rails)



<p class='util--hide'>View <a href='https://learn.co/lessons/optimizing-database-queries'>Optimizing Database Queries</a> on Learn.co and start learning to code for free.</p>
