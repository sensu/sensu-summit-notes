# Displaying metrics in Sensu dashboard
* Which TSDB people use?
	* Mention of moving from Graphite to ElasticSearch 2
	* Prometheus

* It’s possible to preview Graphite graphs directly from Uchiwa: http://roobert.github.io/2014/11/03/Sensu*with*Embedded*Graphite*Graphs/
  * Mention of using images and custom attributes to embed runbooks

* We often forget that the challenge is not only about sending data into a TSDB but actually presenting meaningful data into a dashboard
	* In Grafana, you can use templates for machines so you know what to expect from a certain type of machine. Mentioned example: https://www.youtube.com/watch?v=JR7HZ2LTozg
	* You can use Grafana to represent thresholds so users know what not to cross

* Do people even use the Sensu dashboard?
	* PagerDuty is used to critical alerts
	* ChatBots are used to lower priority alerts
	* It’s hard to remove the noise from the dashboard and see the actual problems
	* If you don’t have an actionnable alert, decrease the criticality of the alert
	* It would be useful to add notes to checks and events without having to silence it

* Does anyone expose a public dashboard to their users?
	* Most people does not
	* Someone has multiple TVs with multiple dashboards but it gets quite overwhelming and little useful
	* Mention of https://github.com/firehol/netdata to explose metrics on every server

* Dashboards should be super simple
	* Not too much and should be readable from a TV
	* Having complex dashboards in Grafana will destroy your TSDB
