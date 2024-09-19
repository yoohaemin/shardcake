# FAQ

### Is the Shard Manager a single point of failure?

Not really. The Shard Manager is a single point of coordination, not a single point of failure.
In fact, 99% of the time, the Shard Manager doesn't do anything. Pods can communicate with each other without needing the Shard Manager.
It is only required when a new pod starts or when an existing pod is removed. In such cases, the Shard Manager reassigns shards to the remaining pods.

You can safely restart the Shard Manager pod without affecting the running pods.

### I get timeouts during a rolling update, what can I do?

The primary recommendation is to check the Shard Manager's logs to see what happens during the rolling update.

A common issue is that stopping pods may not unregister themselves from the Shard Manager. This can occur for several reasons:
- The pod is stopped abruptly without handling the KILL signal, preventing the main fiber from being interrupted.
- The pod loses network connectivity and cannot call the `unregister` endpoint (this can occur when using an Istio proxy, for example).
- The pod is stuck in a deadlock during the shutdown process.
In such cases, it's crucial to understand why the pod isn't unregistering and address the underlying issue.

### Is Shardcake a replacement for Akka/Pekko?

No. Shardcake is a library that covers only a small portion of what Akka/Pekko does, specifically the "Cluster Sharding" feature.
ZIO provides tools for "local" concurrency (e.g., Queue, Hub, Promise), while Shardcake adds the "distributed" component.
However, Shardcake does not address features like event sourcing or actor persistence.

If you need these features, you are encouraged to implement them on top of ZIO and Shardcake.
