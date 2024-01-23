# Rails Checklists

My opinion on developing and running Rails on production, based on my experience. This is a work in progress. I'll be adding more items as I go. If you have any suggestions, please feel free to open an issue or a pull request. I'll be happy to hear from you.

## Keep your gems up to date

Investing in your application by staying up to date with the Rails framework has had a tremendous positive effect on your code base and engineering teams. You'll able to take advantage of new features and improvements and be able to keep your code base clean and maintainable. The same applies to your gems. Keep them up to date. It's not only about security, but also about performance and stability.

## Use profilers

Learn to use profilers like `rack-mini-profiler`, you might don't know that your application is do a lot of work that it shouldn't be doing. Profilers will help you to identify those issues and fix them. Especially when you're facing performance issues. Profilers will help you to identify the bottlenecks, it helps you see what's going on under the hood like database queries, memory allocations, etc.

## Take advantage of the Rails console

The Rails console is a powerful tool. It's not only for debugging, but also for testing and running scripts. You can use it to test your models, run scripts, etc. It's a great tool to have in your toolbox. It also secret for Rails developers to fix issues on production quickly because you can easily run your code on production using the Rails console.

## Reduce the number of queries

This is a common issue that I've seen in a lot of Rails applications. It's very easy to write code that generates a lot of queries. This is especially true when you're using ORMs like ActiveRecord. You should always try to reduce the number of queries that your application generates. You can use tools like `bullet` and `prosopite` to help you identify those issues.

This issue is also known as the N+1 query problem. Rails has a built-in solution for this problem called `includes`. You can use it to eager load associations. If you're not paying attention to this issue, you'll end up with a lot of queries that you don't need and slow down your application.

## Enable strict loading

This is a new feature that was introduced in Rails 6.1. It's a great feature that helps you to avoid N+1 query issues. If you're using Rails 6.1 or later, you should enable it in your application. It's a great feature that helps you to avoid N+1 query at the first place. You'll get an error if you try to access an association that wasn't eager loaded. I like to use it on development and test environments only because I don't want to break my application on production.

## Be careful with accessing associations

Let's say you have a `User` model that has one `Role` model. If you already get the `user` record and you want to get the `role id` of that user, you can do it by `user.role.id`. This will generate a query to get the `role` record. If you only need the `role id`, you can do it by `user.role_id`. This will not generate a query to get the `role` record. This is a very simple example, but it's very common in Rails applications.

## Move heavy work to background jobs

You should always try to move heavy work to background jobs. This will help you to improve the performance of your application. You can use tools like `sidekiq` or `solid_queue` to help you with that. You can also use `ActiveJob` to abstract the background job implementation. You can use it to switch between different background job implementations easily.

Avoid to put objects in the background job arguments. If you need to pass ActiveRecord objects to the background job, you should pass the `id` of the object instead of the object itself because the object might be changed before the background job is executed. You should also avoid to put large objects in the background job arguments because it will increase the size of the background job queue and slow down your application.

## Don't log to disk in production

You should avoid to log to disk in production. It will slow down your application.

## Do mathematical calculations in the database

Sums, averages and more can be calculated in the database. Don’t iterate through ActiveRecord models to calculate data. Use SQL to do the work for you. It will be much faster and more efficient.

## Experiment with different memory allocator

I find that memory used in Ruby program can grow rapidly by the time your application running overtime, until you need to restart your application to free up the memory. One that I personally use is `jemalloc`. It's a general purpose memory allocator that is designed to be scalable and fast. It's used by a lot of companies like Facebook, Twitter, etc. It's also can be used for Ruby on Rails. You can use it to improve the performance of your application. You can also use it to reduce the memory usage of your application. You might be surprised to see how much memory you can save by using it.

## Time.current for time zone aware applications

If you're building a time zone aware application, you should use `Time.current` instead of `Time.now`. `Time.current` will return the current time in the application time zone. `Time.now` will return the current time in the system time zone. If you're using `Time.now` in your application, you might get unexpected results when you change the application time zone. You should always use `Time.current` in your application.

`Time.current` returns `Time.zone.now` when Time.zone or config.time_zone are set, otherwise just returns `Time.now`.

## Enable YJIT

If you're looking for a way to boost your Ruby on Rails application's performance, YJIT could be just the ticket. This Just-In-Time compiler translates your code into machine code on the fly, leading to significant speedups compared to the standard interpreter. YJIT also plays nice with memory, using it more efficiently for large Rails applications that often struggle in this area. And the benefits don't stop there. Startup times are faster, CPU usage can drop, and you'll be future-proofed for upcoming YJIT enhancements

## Use a process supervisor

If you're using Docker to run your Rails application, you should set `dumb-init` as your PID 1. It's a simple process supervisor and init system designed to run as PID 1 inside minimal container environments (such as Docker). It's a great tool that helps you to avoid zombie processes. It also helps you to avoid issues with signals like SIGTERM, SIGINT, etc. You can use it to improve the reliability of your application.

Maybe you don't reliazie it that you have a lot of zombie processes for example chromium that doesn't get killed when your finish your job. You can avoid this by using a process supervisor like `dumb-init` or `tini`.

## Add health check

You should add health check to your application. It's a great way to monitor the health of your application. And you can combine it with docker healthcheck feature to check the health of your application for some interval of time and automatically restart your application if it's not healthy.

## Set Ruby 3.3 as minimum Ruby version

By the time I wrote this, some benchmark shows that Ruby 3.3 combined with YJIT able to achive three times faster than Ruby 2. It's a huge improvement.
