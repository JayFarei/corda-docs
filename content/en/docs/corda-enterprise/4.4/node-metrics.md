---
aliases:
- /releases/4.4/node-metrics.html
date: '2020-01-08T09:59:25Z'
menu: []
tags:
- node
- metrics
title: Metrics
---


# Metrics

A Corda node exports a number of metrics for the purpose of monitoring the health of the node via JMX. This page documents the metrics
exported by Corda.

For more information about how to monitor a node, see node-administration.


## Attachments


{{< table >}}

|Metric Query|Description|
|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
|net.corda:name=Attachments|A count of the total number of attachments on the node|

{{< /table >}}


## Caches

A Corda node maintains a number of caches. For each of the metrics below, the name of the cache must be supplied in the component field to
show metrics for that cache. There are two sorts of caches: size-based and weight-based. Size-based caches are measured in the number
of entries in the cache, while weight-based caches are measured in the bytes of memory occupied by the entries. Note that the set of metrics
available depends on the cache type. Maximum-size and sizePercent is only available for size-based caches, while maximum-weight, weight, and
weightPercent are only available for weight-based caches.


{{< table >}}

|Metric Query|Description|
|-------------------------------------------------------------------|--------------------------------------------------------------------------------------|
|net.corda:type=Caches,component=<cache_name>,name=evictions|The number of items evicted from the cache|
|net.corda:type=Caches,component=<cache_name>,name=evictions-weight|The total weight of items evicted from the cache|
|net.corda:type=Caches,component=<cache_name>,name=hits|The number of cache hits|
|net.corda:type=Caches,component=<cache_name>,name=loads|Histogram indicating how long loads into the cache are taking|
|net.corda:type=Caches,component=<cache_name>,name=loads-failure|The number of items that could not be loaded into the cache|
|net.corda:type=Caches,component=<cache_name>,name=loads-success|The number of items successfully loaded into the cache|
|net.corda:type=Caches,component=<cache_name>,name=maximum-size|The maximum number of entries in the cache|
|net.corda:type=Caches,component=<cache_name>,name=misses|The number of cache misses|
|net.corda:type=Caches,component=<cache_name>,name=size|The current number of entries in the cache|
|net.corda:type=Caches,component=<cache_name>,name=sizePercent|The current size of the cache expressed as a percentage of the maximum|
|net.corda:type=Caches,component=<cache_name>,name=maximum-weight|The maximum size of the cache, expressed as a total weight|
|net.corda:type=Caches,component=<cache_name>,name=weight|The current weight of the cache|
|net.corda:type=Caches,component=<cache_name>,name=weightPercent|The current weight of the cache, expressed as a percentage of the maximum|

{{< /table >}}


## Flows


{{< table >}}

|Metric Query|Description|
|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
|net.corda:type=Flows,name=ActiveThreads|The total number of threads running flows|
|net.corda:type=Flows,name=CheckpointVolumeBytesPerSecondCurrent|The current rate at which checkpoint data is being persisted|
|net.corda:type=Flows,name=CheckpointVolumeBytesPerSecondHist|Histogram indicating the rate at which bytes are being checkpointed|
|net.corda:type=Flows,name=Checkpointing Rate|The rate at which checkpoint events are occurring|
|net.corda:type=Flows,name=Error|The total number of errored flows|
|net.corda:type=Flows,name=Finished|The total number of completed flows (both successfully and unsuccessfully)|
|net.corda:type=Flows,name=InFlight|The number of in flight flows|
|net.corda:type=Flows,name=QueueSize|The current size of the queue for flows waiting to be executed|
|net.corda:type=Flows,name=QueueSizeOnInsert|Histogram showing the queue size at the point new flows are added|
|net.corda:type=Flows,name=Started|The total number of flows started|
|net.corda:type=Flows,name=Success|The total number of successful flows|

{{< /table >}}


## Metering


{{< table >}}

|Metric Query|Description|
|-----------------------------------------------|---------------------------------------------------------------------------------------|
|net.corda:type=Metering,name=commandsPersisted|The number of unique sets of commands persisted|
|net.corda:type=Metering,name=droppedCounts|The number of signing events not persisted|
|net.corda:type=Metering,name=queueLength|Histogram indicating the length of the queue of events waiting to be persisted|
|net.corda:type=Metering,name=stacksPersisted|The number of unique CorDapp stacks persisted|
|net.corda:type=Metering,name=totalCounts|The total number of signing events persisted|

{{< /table >}}


## P2P


{{< table >}}

|Metric Query|Description|
|----------------------------------------------|-----------------------------------------------------------------------------------------------------------|
|net.corda:type=P2P,name=ReceiveDuration|Histogram measuring latency between receiving a P2P message and delivering it to the state machine|
|net.corda:type=P2P,name=ReceiveInterval|Histogram measuring the interval between received P2P messages|
|net.corda:type=P2P,name=ReceiveMessageSize|Histogram measuring the size of received messages|
|net.corda:type=P2P,name=SendLatency|Histogram measuring latency when sending P2P messages, between send and send acknowledge by Artemis|
|net.corda:type=P2P,name=SendMessageSize|Histogram measuring the size of sent messages|
|net.corda:type=P2P,name=SendQueueSize|The size of the in-memory send queue in the state machine for messages waiting to be sent to Artemis|
|net.corda:type=P2P,name=SendQueueSizeOnInsert|Histogram measuring the size of the in-memory send queue in the state machine when new messages are added|

{{< /table >}}

