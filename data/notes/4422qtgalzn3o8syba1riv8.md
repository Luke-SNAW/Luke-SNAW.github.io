
> https://www.moderntreasury.com/journal/shifting-our-apis-pagination-method-from-offset-to-cursor-based

# deferred join

There are ways to mitigate the (although not eliminate) the slowing down of offset/limit pagination in later pages. The technique is called a "deferred join" and it is most effective in MySQL. The basic idea is to paginate as little data as necessary, and then do a self-join to get the rest of the data for a single page.

You can read more about it [here](https://aaronfrancis.com/2022/efficient-pagination-using-deferred-joins) or [here](https://planetscale.com/blog/fastpage-faster-offset-pagination-for-rails-apps).

There are libraries for [Laravel](https://github.com/hammerstonedev/fast-paginate) and [Rails](https://github.com/planetscale/fast_page) as well!

Cursor based pagination is wonderful, but sometimes you're stuck with offset/limit for whatever reason. Might as well make it fast.

## mostly only works in MySQL

To be clear, this technique (which it seems I independently discovered in 2015) mostly only works in MySQL because other databases usually have planners which are smart enough to not pull everything in eagerly.

MySQL is fairly predictable, though, so when you understand that it wants to nested-loop join all your rows before evaluating predicates on the parent table, it's a predictable win to stop it doing that.

The technique is still applicable even when you have no joins, because MySQL will materialize rows with every selected column before evaluating the unindexed portion of the predicate, and the order by.

# keyset pagination

My favourite technical explanation of that is [here](https://use-the-index-luke.com/no-offset)

# Why does every web site default to aggressively paginate their information?

Pagination sucks, it's a waste of time and of clicks, and should be a last resort. Sure, when Google returns millions of search results, paginate. But:
For instance, if you have 40 entries and specify that there should be 10 items per page

40 entries??? Just show them all to me. My browser has a scrollbar, CTRL-F is much faster than your search box.

"but not everyone has a reliable fast connection" -- yes, which is a good reason to deliver more data per http request than breaking it up and requiring lots of slow requests.

"but the database load" -- half the queries, each returning 2x data, is almost always going to be easier on a RDBMS. If it's not then you probably need to rethink your schema.

## marketing

> Why does every web site default to aggressively paginate their information?  
> You get to see more ads while flipping through pages.

Timing metrics for loading smaller pages make marketing happy.

Timing metrics for time spent on the website make marketing happy.
