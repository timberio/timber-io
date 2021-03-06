---
breadcrumbs: Timber for Heroku / Events & Context
title: server_memory_sample event
formatted_title: <i class="fa fa-cube" aria-hidden="true"></i> <code>server_memory_sample</code> event
toc: true
---

By enabling Heroku's [log runtime labs feature](https://devcenter.heroku.com/articles/log-runtime-metrics)
memory samples will be periodically dumped into your logs. Timber recognizes and parses these events
as `event.server.cpu_sample`.

```
source=web.1 dyno=heroku.2808254.d97d0ea7-cf3d-411b-b453-d2943a50b456 sample#memory_total=21.00MB sample#memory_rss=21.22MB sample#memory_cache=0.00MB sample#memory_swap=0.00MB sample#memory_pgpgin=348836pages sample#memory_pgpgout=343403pages
```

### Example JSON Structure

```json
{
  "event": {
    "server": {
      "memory_sample": {
        "cache_mb": 100,
        "limit_mb": 512,
        "pgpin": 200,
        "pgpout": 150,
        "rss_mb": 100,
        "swap_mb": 100,
        "totla_mb": 100
      }
    }
  }
}
```

### Field descriptions

Name | Type | Description
-----|------|------------
`cache_mb` | `number` | The portion of the memory used for disk cache. `minimum: 0`
`limit_mb` | `number` | The maximum amount of memory, limit, that can be used before swap is used. `minimum: 0`
`pgpgin` | `number` | The cumulative total of the pages read from disk. Sudden high variations on this number can indicate short duration spikes in swap usage. The other memory related metrics are point in time snapshots and can miss short spikes. `minimum: 0`
`pgpgout` | `number` | The cumulative total of the pages written to disk. Sudden high variations on this number can indicate short duration spikes in swap usage. The other memory related metrics are point in time snapshots and can miss short spikes. `minimum: 0`
`rss_mb` | `number` | The portion of the memory being used by the target application. `minimum: 0`
`swap_mb` | `number` | The portion of the memory stored on disk. Swap usually indicates a shortage of memory. `minimum: 0`
`total_mb` | `number` | The sum of the rss, cache, and swap that equals the total memory being used. `minimum: 0`

### Using this data

Example queries:

* Full path: `event.server.memory_sample.rss_mb:>100`
* Short path: `memory_sample.rss_md:>100` - Short paths are aliases allowing for simpler access to these fields.
* Only this event: `is:exception`


See our doc on [using context & event data]({% link _docs/app/basics/events-and-context.md %}#what-can-i-do-with-this-data).
