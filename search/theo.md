# Search

I suggest we use Mongo to store, query and search message. It's an easy solution that's not hard to deploy, not hard to code for.

For files, I'm not sure. Either an S3, or what our Ceph offers: filesystem, block or object storage...

---

Having one database to store AND index messages avoids having to code for two different systems/SDKs, and copy-pasting all msg data all the time in another "indexation" database (it would be the same data, but in 2 different places).

-> When we will need better performance, we can then make another architecture decision to upgrade the search engine tech and deployment.

# Motivation

We have to store:

- Files -> Object storage or filesytem
- Messages -> Documents (may or may not have X files linked, pinned status etc)

I believe we have the following options:

- Storing messages for read/write AND indexing in the same database (must be a good one then).
- Storing messages in two databases, one for read/write, one for indexing that can be deferred (doesn't have to be very real-time)
- For files, storing them in a S3 or filesystem. Maybe our underlying Ceph.

I have considered Elasticsearch (DX not good, too resource hungry), Mongodb, MinIO, Deuxfleur's Garage, SQL databases.
