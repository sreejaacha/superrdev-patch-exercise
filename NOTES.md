\# Notes



\## Summary of changes

\- Fixed AND/OR precedence in the search SQL (repository, db/queries, and both queries in the Oracle package). Archived tasks were leaking into results and the status filter was ignored for title matches.

\- Removed an artificial Thread.sleep in TaskController that slowed short searches.

\- Invalid status now returns 400 instead of a 500 error.

\- Added guards for page and pageSize values.

\- Fixed useTasks hook: loading now resets on error, errors are cleared, and old responses are ignored (race condition).

\- Added 300ms search debounce and reset to page 1 when filters change.



\## What I chose not to change

\- Pagination still happens in memory. Changing to database paging is a bigger change than this timebox needed.

\- LIKE wildcards (% and \_) are not escaped. Low impact for an internal tool.

\- No indexes added, as the data set is small.



\## Biggest remaining risk

Loading all matching rows and slicing in Java will get slow and use lots of memory as the table grows.



\## Tools used

I used Claude to help find the bugs and draft the fixes. I then ran the app, tested each fix myself, and wrote the handwritten explanations on my own.

