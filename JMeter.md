To load JMeter output into Logstash and aggregated in Elasticsearch so that Kibana can display analytics graphs:

What I’m hoping for is a single/few graph in Kibana that illustrates test run conclusions:

* <strong>Network variation</strong> based on response time reaching landing page only.
* <strong>Capacity identification</strong> from stress test runs (showing transactions per minute vs. response time)
* <strong>Capacity usage</strong> based on memory per user over time.
* <strong>Longevity</strong> showing memory leaks based on

## Resources:
http://theworkaholic.blogspot.in/2015/05/graphs-for-jmeter-using-elasticsearch.html

http://blog.sematext.com/2015/06/23/replaying-elasticsearch-slowlogs-logstash-jmeter/
