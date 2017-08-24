
# Metrics discussion - types, storage, pain points, containers

## Questions/pain points

**Metrics data storage**
* how do we store data into graphite from sensu?*
	* Eric: extension/handler built into sensu, send output to graphite endpoint
* Checks are available that are designed for this (key/value/timestamp)
* InfluxDB also has extensions available (written in go, easy to stand up, scalable), has tags
* Elastic search is another option
* diff between handler & extension: extension runs in ruby runtime so it’s more efficient for rapid data like this, handler forks and is less ideal
* grafana is the easiest to work with for these database

**What about business metrics? Can we do this too?**
* Yes, to the extent we can pull business metrics out of server activity such as access logs
* Capacitor - from Influx people, does predictive analysis and allows complex logic, trend analysis, to do alerting
* Grafana can also trigger alerts now as of v4
* Sensu can be setup to check TSDB metrics and alert based on them


**Why use sensu for this?**
Benefits
* rabbitmq provides good transport already
* utilize existing infrastructure to get metrics routed in complex environments.  Just setup for sensu and then setup sensu to talk to graphite (1 channel for everything).  Simplifies routing and communications across the environment
Drawbacks
* what if sensu dies?  will get get notified?
    * recommend some additional system monitors basics likes heartbeats and/or sensu functionality, pingdom checks, etc

**Pain points:**
* We run two checks now, one for alerting and another for metrics.  Maybe it should just be an element of the payload on the check.
* Enterprise allows for contact groups which can help to route different metrics to different graphite instances for multitenancy
* Eric - cpu usage for metrics on tiny instances like t2.micro can use a lot of the system resources
* solved by using Telegraph which is more lightweight

**Kubernetes & Prometheus:**
* How do we get data into the sensu stream?
	* can expose a json hash which a sensu check can scrape
	* you can push or pull, statsd is good for sending
	* use sidecars
	* push from application to local sockets on the kubernetes/docker hosts where sensu can run more natively

**Predictive analytics:**
* hard to do, data science people help a lot here
* some projects around this but it’s not especially user friendly for non-statistics-nerds

**sensu 2.0 metrics stuff:**
* view metrics live in dashboard as well as connect to TSDBs
* goal is not to build a new TSDB but utilize existing ones
* not clear what the goal will be, do they replace grafana or integrate?  they haven’t decieded yet
