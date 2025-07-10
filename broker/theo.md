# broker technology

Decision: Not sure.

I know Kafka, managing it is meh, coding with it is okay.

I don't know RabbitMQ, I'd need to POC it.

There's also pravega, pulsar, and maybe others that I know nothing about.

## Rationales

We may not need ultra super duper low latency and ultra mega scalability.

We may want to persistently store messages, 1) to not lose them in the event of a catastrophe and 2) to aggregate them into a mongodb/other database before deleting them from the broker. To do CQRS, search, backups or whatever.
