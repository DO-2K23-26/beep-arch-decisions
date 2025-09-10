# broker technology And data format

I recommend RabbitMQ with protobuf, _without_ a remote registry.

## Broker rationale

Kafka is bad on Ops level at least. Config, deploy, management...
Supposedly RabbitMQ is easier on that level at least.
There's also other stuff to look into: pravega, pulsar, and maybe others that I know nothing about.

We may not need ultra super duper low latency and ultra mega scalability.

We may want to persistently store messages, 1) to not lose them in the event of a catastrophe and 2) to aggregate them into a mongodb/other database before deleting them from the broker. To do CQRS, search, backups or whatever. But this is just possible future work - would work with any broker.

Ease of development, dev env and prod.

Learning a second brokering tech, I consider vital, and this is an opportunity.

---

As for the data format:

I recommend Protobuf. My experience with it has proven to me that it is just as simple to ser/deserialize than JSON in code using existing libs, but has the following advantages:

- Very human readable language definition, with clear types(!) -> The deser. receiver/programmer makes no assumption about the types.
- Enforces defining your interface and managing it - I consider this vital in a microservices env.
- Provides idiomatic features for retro- and forward-compatibility of API interfaces through enforced numbering of the message fields (which, combined with the clear types. also makes breaking changes very clear)
- Better performance through a well made binary compression - Though that's not the most relevant for us.

Note that I recommend Protobuf files to be versioned _in the code_, not deployed in a remote, self-managed registry on the network/in the cluster.
This makes no Ops overhead, and APIs don't break thanks to language features (excepting API breaking changes, ofc)
