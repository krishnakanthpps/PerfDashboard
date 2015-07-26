To load JMeter output into Logstash and aggregated in Elasticsearch so that Kibana can display analytics graphs:

What I’m hoping for is a few graph in Kibana that illustrates test run conclusions:

1. <strong>Network variation</strong> based on response time reaching landing page only.
2. <strong>Landing page capacity</strong> transactions-per-second maximum.
3. <strong>Sign-Up capacity</strong> showing how many new users can register in a short period of time.
4. <strong>Ramp-up capacity</strong> showing how many registered users can do work at once based on 
   stress test runs (showing transactions per minute vs. response time).
5. <strong>Capacity usage</strong> based on memory per user over time.
6. <strong>Longevity</strong> showing memory leaks identified during longer runs.

## Resources:
http://theworkaholic.blogspot.in/2015/05/graphs-for-jmeter-using-elasticsearch.html

http://blog.sematext.com/2015/06/23/replaying-elasticsearch-slowlogs-logstash-jmeter/
