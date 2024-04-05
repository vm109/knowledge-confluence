### Elasticsearch Disk Space Issue, single shard on single node caused this issue
- The Elasticsearch disk space ran out, causing shard reallocation across the cluster.
- Setting up only one shard per node led to an excessive number of writes on a single node, depleting its disk space and triggering a cascade effect.
- It's advisable not to limit the system to one shard per node; instead, increasing the number of shards can prevent such issues.
- Autoscaling might be a viable solution to dynamically adjust resources and prevent disk space shortages. 
