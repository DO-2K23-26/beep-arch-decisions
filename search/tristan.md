# Proposal - Search Engine for Beep

> TLDR : Quickwit is a lightweight + powerful search engine that can use s3 (minio or garage) for storage

## Needs

Beep needs a search engine to perform full text searches on several entities in the system.
1. At the server level, we need to be able to retrieve a message from a server across all the channels.
2. At the platform level, users need to be able to find a **public** server based on its name/description. This use-case is a little bit trickier because several servers might fit the research and some might be more relevant than others.

## Proposal

[Quickwit](https://quickwit.io/) is a search engine written in rust that can use any filesystem/s3-compatible storage to store indexes. Quickwit is thus way lighter than Elastic Search and Solr since both are written in Java and known to be real memory nightmares.

We could use either [Minio](https://github.com/minio/minio) or [Garage](https://github.com/deuxfleurs-org/garage) for on-premise index storage. I don't really have an opinion on that even though I think that Garage would be a better fit since [Minio's change of License](https://min.io/compliance).

### Drawback(ish)

Quickwit doesn't provide a SDK in a specific programming language, it only exposes a [REST API](https://quickwit.io/docs/reference/rest-api). There will be some plumbing to do to adapt Quickwit to the language/languages that we pick for Beep. But this also means that we aren't blocked by an unusable/inexisting SDK (e.g. Solr in Rust). Also, quickwit provides an [Elastic-Search compatible API](https://quickwit.io/docs/reference/es_compatible_api) meaning that we could use any Elastic search client with Quickwit, however this API is still work in progress and thus might not provide all the features of Elastic Search.


## Features

- [Partitionning for multi-tenant applications](https://quickwit.io/docs/overview/concepts/querying#partitioning) - optimizes performances for searches with a lot of servers since each server is "isolated".
- [Scoring algorithm for relevancy sorting](https://quickwit.io/docs/overview/concepts/querying#scoring) - already implements a ranking score which could be really useful for the discovery of new public servers when joining the platform.

## References

- [POC using quickwit for message indexation in Golang](https://github.com/Courtcircuits/tad-beep/tree/main/pocs/inter-service/messages/infrastructure/quickwit)
- [Quickwit documentation](https://quickwit.io/docs/get-started/quickstart)
- [Talk about Quickwit](https://www.youtube.com/watch?v=s_C8O5ecZBE)

> For the record, Teychene recommended me to use Quickwit (this guy worked for Elastic).
