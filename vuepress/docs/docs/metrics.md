# Metrics

Shardcake exposes a few metrics to give you better visibility into the state of your cluster.
Those metrics are exposed via [ZIO Metrics](https://zio.dev/reference/observability/metrics/), which allows you to use the [backend of your choice](https://zio.dev/zio-metrics-connectors/).

## Shard Manager Metrics
- `shardcake.pods` (gauge): Number of pods currently registered
- `shardcake.shards_assigned` (gauge): Number of shards currently assigned to a pod
- `shardcake.shards_unassigned` (gauge): Number of shards currently not assigned to any pod
- `shardcake.rebalances` (counter): Number of rebalances that have occurred
- `shardcake.pod_health_checked` (counter): Number of times the health of a pod has been checked

## Pod Metrics
- `shardcake.shards` (gauge): Number of shards currently assigned to the pod
- `shardcake.entities` (gauge): Number of entities currently running on the pod
- `shardcake.singletons` (counter): Number of singletons currently running on the pod
