This repo contains notes, configuration, and source files on creating a way to analyze
with <strong>only free/open source software</strong>. The components include the 
"ELK" stack, where stands for Elasticsearch Logstash Kibana:


1). Github for documentation and source control.

2). JMeter to create load on the system artificially by using Java programs to 
    emulate many real clients.

3). Maven to package java

4). Puppet to manage configurations

5). Docker 

6). <a href="#Logstash">Logstash</a> collects timestamped logs of
   <a href="#LogFormats">various formats</a>, from
   <a href="#LogSources">various sources</a>, parse to filter out junk, index them, and normalize into JSON
   in a way that's searchable in a central location. 
   Better than awk, grep, etc. on individual machines.

7). <a href="LogstashForwarder"> Logstash Forwarder</a> to direct log entry flow within internet-scale production environments.

8). RabbitMQ queue services between Logstash producers and consumers to ensure scalability
   by absorbing spikes.

9). <strong>Elasticsearch</strong> indexes (inverted) nested aggregations of data in Hadoop.

10). <strong>Curator</strong> at https://github.com/elasticsearch/curator
   to manage our Elasticsearch indexes
   by enabling admins to schedule operations to optimise, close, and delete indexes.

11). <strong>Kibana</strong> does data discovery on elasticsearch cluster to identify "actionable insights"
   and presents visualization (a dashboard).
   
12). An alerting sytem.



## <a name="Why"> Why</a>
Elasticsearch provides consistency to different time stamp formats.

Kibana "democratizes" data by putting a front-end to access data
in a searcheable in fast a meaningful ways.



## <a name="Managers"> Managers</a>
1. To manage Logstash ???

3. To manage Kibana ???


## <a name="Docs"> Documentation</a>
https://www.elastic.co/guide/en/elasticsearch/guide/current/index.html
The Definitive Guide to Elastisearch you can submit updates at
https://github.com/elastic/elasticsearch-definitive-guide

There is a lighter edition of Logstash.

Kibana & Elasticsearch started as an open source project, built by devops people for devops people.

  * https://github.com/elastic/elasticsearch
  * https://github.com/elastic/kibana
  * https://github.com/elastic/logstash was begun by @jordansissel while at Dreamhost, who continues to create videos
    https://www.youtube.com/channel/UC1Hc-GPNTYax-vAVCH333ww as Elastic employee.
    His talk: https://www.youtube.com/watch?v=fwMnb4-t8vo

 * https://github.com/docker-library/kibana


## <a name="Pricing"> Pricing</a>
It's priced by node to be managed and monitor at scale (less than Splunk and doesn't run out of gas).
There's no separate enterprise edition.

Marvel is free until production.
Unlike Splunk, where it's expensive (millions) after the first 500 MB of free.


## <a name="Competitors"> Competitors</a>

Competitors to Logstash include 
* Flume+Elasticsearch+Kibana or Flume+HDFS+HIVE+PIG
* Greylog2
* Fluentd+MongoDB
* [Stackify](http://stackify.com/smart-error-log-management-trial-sign)
* LOGalyse 
* Scribe


## <a name="CompetitiveFeatures"> Competitive Features</a>
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


## <a name="Versions"> Verions</a>
Version 4 was a major upgrade than version 3.

Logstash v1.5


## <a name="DownloadInstaller"> Download Installer</a>
Kibana installs with its own Node.js server. It doesn't use a web server.

A single node is a master, data, and client nodes.
A node specializes into data and client nodes.

Configure Elasticsearch at 
http://jakege.blogspot.sg/2014/03/how-to-install-elasticsearch.html

Configure for scale by using a Logstash Forwarder and RabbitMQ between a Logstash Producer and Logstash Consumer
http://jakege.blogspot.in/2014/04/centralized-logging-system-based-on.html


### <a name="Docker"> Docker package</a>



## <a name="Logstash.conf"> Logstash.conf</a>
The most basic configuration file:

```
input { stdin { } }
filter {
   grok {
      type => "apache"
      pattern ==> ['%{COMBINEDAPACHELOG}']
   }
}
output {
  stdout { codec => rubydebug }
  elasticsearch { embedded => true }
}
```

## <a name="LogstashForwarder"> Logstash Forwarder</a>
Logstash Forwarder is written in Go.



### <a name="LogSources"> Logstash Sources</a>

Logs into Logstash <strong>brokers</strong> can be from various <strong>shippers</strong> (origins):
* TCP/UDP
* Files
* Syslog
* Microsoft Windows Eventlogs
* STDIN
* WebSockets
* ZeroMQ
* Twitter
* SNMPTrap
* geoIP

Brokers go to Lucene <strong>index</strong> accessed by the storage and search server
which has a web interface.

The lifecycle of a log: Record, Transmit, Store, Delete.

## <a name="LogFormats"> Log Input Formats</a>,
Data Formats:
* JSON
* XML
* CSV
* Multi-line stack traces
* Regex
* Grok (Regex on steroids)
* Zabbix
* SQS (Amazon)

Logstash normalizes different timestamps into your format.


### <a name="LogOutputs"> Log Outputs</a>,

* TCP/UDP
* Email
* Files
* HTTP
* Nagios monitoring
* Alerting tools (Hipchat, SMS)
* Graphic suites (StatsD, Graphite)


### <a name="Filters"> Filters</a>
labls instead of regex patterns.


## <a name="LogstashInstall"> Logstash Install</a>
A sample using the .conf files described above:

```
#install logstash (based on http://jakege.blogspot.in/2014/04/centralized-logging-system-based-on.html)
sudo wget https://download.elasticsearch.org/logstash/logstash/logstash-1.3.3-flatjar.jar
sudo mkdir /opt/logstash
sudo mv logstash-1.3.2-flatjar.jar /opt/logstash/logstash.jar
sudo wget http://logstash.net/docs/1.3.2/tutorials/10-minute-walkthrough/hello.conf
sudo wget http://logstash.net/docs/1.3.2/tutorials/10-minute-walkthrough/hello-search.conf
sudo mv hello.conf /opt/logstash/hello.conf
sudo mv hello-search.conf /opt/logstash/hello-search.conf
cd /opt/logstash/
#example configuration
java -jar logstash.jar agent -f hello.conf
java -jar logstash.jar agent -f hello-search.conf
```

The java here is a JRuby run-time (for performance).
Logstash is extendable with Ruby.


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

* at Elasticsearch
  https://www.youtube.com/watch?v=Epe63Uu-IO0&spfreload=1
  Mar 17, 2015

* Andrew Puch @gmail 
https://www.linkedin.com/in/apuch
who runs http://andrewpuch.com/
and the #devopsengineers Slack channel at http://devopsengineers.com/
created as https://twitter.com/awstutseries
https://www.youtube.com/watch?v=ge8uHdmtb1M
which details how to setup Elasticsearch.

* Steve Mayzak-Director of Sales Engineering @ ElasticSearch
did https://www.youtube.com/watch?v=uxfvNwl_MGc
What is ELK and how can it help you discover, visualize and analyze your data?
Oct. 14, 2014

* Tim and Anna Roes in Germany:
https://www.timroes.de/2015/02/07/kibana-4-tutorial-part-1-introduction/

* Jeff Sogolov: 
  https://www.youtube.com/watch?v=Kqs7UcCJquM
  Visualizing Logs Using ElasticSearch, Logstash and Kibana
  May 16, 2014

* Agitare Technologies
https://www.youtube.com/watch?v=uxfvNwl_MGc
What is ELK and how can it help you discover, visualize and analyze your data?

* Spencer Alger (@spencerAlger) 
  His intro to the ELK Stack Feb 25, 2015
  https://www.youtube.com/watch?v=QyWZ_wQEM9k
  He works on JS libraries at Elastic
  http://github.com/spalger

* James Turnbull (at Kickstarter)
  wrote $9.99 The Logstash v1.5 Book Kindle Edition
  http://www.amazon.com/Logstash-Book-James-Turnbull-ebook/dp/B00B9JQTCO/ref=wilsonslifenotes

*  Alberto Paro wrote
   ElasticSearch Cookbook $20.44
   http://www.amazon.com/ElasticSearch-Cookbook-Alberto-Paro/dp/1782166629
   
* Clinton Gormley and Zachary Tong
  Elasticsearch: The Definitive Guide Feb 7, 2015 $22.55
  http://www.amazon.com/Elasticsearch-Definitive-Guide-Clinton-Gormley/dp/1449358543/

* Radu Gheorghe (Author), Matthew Lee Hinman  (Author), & 1 more
  Elasticsearch in Action Paperback – August 31, 2015
  http://www.amazon.com/Elasticsearch-Action-Radu-Gheorghe/dp/1617291625/

## <a name="Social"> Social</a>
https://github.com/markwalkom/kibana-dashboards
A collection of Kibana dashboards from the community

http://www.theagileadmin.com/2010/08/20/logging-for-success
