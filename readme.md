README
======

This version of Elasticsearch is based on the v1.0.0 release from Github. It includes additional logging code inserted at various points in the code to track the duration of the search phases inside Elasticsearch. The target is to keep it up to date with the latest ES release being used by Waldo and Hugo.

A single static logger, `com.meltwater.metrics.MetricsLogger` is used for logging. Currently it uses log4j for configuration but can be extended to use our statsd based remote logging system as well. Each log entry is tied to a shard action via the shard id and also includes phase information through text. The shard ids are specific to each search request - response cycle.

The following activities are being logged

1. Start and end of a `TransportSearchAction` that is an entry point to the code after network activities have concluded
2. The first of search action
    * The index selection activity
    * The initial collection of document ids
3. The second phase of search action
    * The query phase
    * The fetch phase

  