This will host a Grafana clone that does what you need and nothing else.

Only configurable via source. I.e. only the bits you *like* from Grafana.

Text below is how something like this can look:

# Spartana: A Simplified Grafana

Goal: a minimal dashboarding solution that is 100% provisioned via files. There is no U/I to add
dashoards on the fly. KISS and the Unix philosophy, etc.

* A Go package, that contains the dashboard definitions, either see what Grafana has or
  cleanup: <https://github.com/grafana-tools/sdk>
* Dashboards are defined in (minimal) YAML
* Templating is supported, variables are supported
* Dashboards are put in folders and may have tags, this is all defined in the dashboard itself
* Everything is defined on a per-dashboard basis
* Only support a subset of graphs:
  * graphPanel
  * tablePanel

  No: singlestats, alertlist, etc.

* No plugins for new types of panels; how and if new panels are going to be supported is an open
  question
* No alerting, we have alertmanager for that.
* *Left align* the Graphs on a page
* No auto-reloading
* Only support Prometheus as a data source
* No user management; only allow anonymous access; everything is public
* Apache license

## How

We can fork Grafana and rip out all the bits we don't need or just start from scratch. We have such
modest requirements that starting from scratch might be the better path forward. We can then just
copy the best ideas from Grafana.

## Libraries

Just a list, haven't vetted some of them:

* Go graphing pkg: <https://github.com/go-graphite/carbonapi/tree/master/expr/functions/cairo/png>
  (Haven't looked closely)
* Graphing lib for the browser: <https://developers.google.com/chart> (I find this one promising)
* InfluxDBs graphing code <https://github.com/influxdata/giraffe>

## Spartana/grafana

The [spartanaorg/grafana](https://github.com/spartanaorg/grafana) is the current playground, for (at
first) removing things; once that is small enough we'll copy it to *spartana* and call it out first
release.

Currently remove from *Grafana* upstream:

* users - there is no auth anymore - everyone is Admin (although that has no meaning anymore).
* alerting - prometheus alertmanager is the only one left.
* Go vendoring has been removed.
