
How to store stuff and make sense of 
The "ELK" stack (for Elasticsearch Logstash Kibana) really should be LEK because 

1. <strong>Logstach</strong> collects timestamped logs from 
   <a href="#LogSources">various sources</a>, parse to filter out junk, index them, and normalize into JSON
   in a way that's searchable in a central location.

2. <strong>Elasticsearch</strong> indexes (inverted) nested aggregations of data in Hadoop

3. <strong>Kibana</strong> does data discovery on elasticsearch cluster to identify "actionable insights"

But LEK doesn't spell and pronounce like a one-syllable name for a big animal with a big rack.
(actually that was taken for something else).

## <a name="Docs"> Documentation</a>
https://www.elastic.co/guide/en/elasticsearch/guide/current/index.html
The Definitive Guide to Elastisearch you can submit updates at
https://github.com/elastic/elasticsearch-definitive-guide

There is a lighter edition of Logstash.

Kibana & Elasticsearch started as an open source project, built by devops people for devops people.

  * https://github.com/elastic/elasticsearch
  * https://github.com/elastic/kibana
  * https://github.com/elastic/logstash
 
 * https://github.com/docker-library/kibana

It's priced by node to be managed and monitor at scale (less than Splunk and doesn't run out of gas).
There's no separate enterprise edition.

Marvel is free until production.

Version 4 was a major upgrade than version 3.

* D3 JS library flexibility
* Watcher - 
* Shield support for security


* Bulk operations (for indexing and search operations)
* Percolator ("reversed search" - alerts, classification)
* Suggesters ("Did you mean ...?")
* Index aliases (Grouping, filtering or "renaming" of indices every day)
* Index templates (automatic index configuration)
* Monitoring API (amount of memory used, number of operations, etc.)

* Pie charts have nested levels


## <a name="DownloadInstaller"> Download Installer</a>
Kibana installs with its own Node.js server. It doesn't use a web server.

A single node is a master, data, and client nodes.
A node specializes into data and client nodes.

## <a name="LogSources"> Sources</a>,
Logs into Logstash can be from:
* TCP/UDP
* Files
* Syslog
* Microsoft Windows Eventlogs
* STDIN
* WebSockets
* zeromq

Extendable with Ruby (JRuby run-time).

Data Formats:
* JSON
* XML
* CSV
* Multi-line stack traces
* Regex
* Grok (Regex on steroids)


## <a name="Demo"> Demo</a>
  * https://github.com/elastic/demo
 used Virtualbox and Vagrantup.


## <a name="Scaling"> Scaling</a>
To scale, brokers:
* 
* Kafka reindexes everything.

For more scale, between intermediate brokers are
* Storm
* Spark cache
* Samza

Flume can send to HDFS for es-hadoop


## <a name="RockStars"> ELK Rock Stars</a>
This tutorial was based information from these people and their work:

Andrew Puch @gmail 
https://www.linkedin.com/in/apuch
who runs http://andrewpuch.com/
and the #devopsengineers Slack channel at http://devopsengineers.com/
created as https://twitter.com/awstutseries
https://www.youtube.com/watch?v=ge8uHdmtb1M
which details how to setup Elasticsearch.


Steve Mayzak-Director of Sales Engineering @ ElasticSearch
did https://www.youtube.com/watch?v=uxfvNwl_MGc
What is ELK and how can it help you discover, visualize and analyze your data?
Oct. 14, 2014

Tim and Anna Roes in Germany:
https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-1-introduction/


## <a name="Social"> Social</a>
https://github.com/markwalkom/kibana-dashboards
A collection of Kibana dashboards from the community

