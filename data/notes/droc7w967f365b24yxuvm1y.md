
- [Many Small Queries Are Efficient In SQLite](https://www.sqlite.org/np1queryprob.html)
- [Absurd Success](https://www.marginalia.nu/log/87_absurd_success/)
  > The author describes making several improvements to their search engine that significantly increased its performance and scalability. They reworked the URL database to use a single SQLite table instead of large MySQL tables, generating unique IDs during indexing rather than relying on database auto-increment. This reduced RAM usage and allowed indexing to continue while the database was updated. They also changed how the reverse index was constructed, building multiple smaller pre-indexes in memory and then merging them, instead of using a large in-memory lexicon. This avoided writing terabytes of random data to disk and allowed indexing disparate datasets together. Overall these changes halved RAM usage and addressed all known scaling issues, improving the system considerably more than expected.
- [BIG DATA IS DEAD](https://motherduck.com/blog/big-data-is-dead/)
  > The author suggests that the real problem is often data hoarding rather than true "Big Data" challenges. Overall, the passage contends that the Big Data hype has passed and organizations should focus on using their data effectively rather than worrying about sheer data volume.
- [SQLite As An Application File Format](https://www.sqlite.org/aff_short.html)
- [SQLite-on-the-Server Is Misunderstood: Better At Hyper-Scale Than Micro-Scale](https://rivet.gg/blog/2025-02-16-sqlite-on-the-server-is-misunderstood)
