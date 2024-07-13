# learn-cloudwatch-log-insights-query
How to run sql query for cloudwatch log insights

How to find flow logs that has 10.123.85.100 for ports 8834 and REJECT response
```ruby
fields @timestamp, @message, @logStream, @log
| filter @message like /10\.123\.85\.100/ and @message like /8834/ and @message like /REJECT/
| sort @timestamp desc
| limit 1000
```
```bash
fields @timestamp, interfaceId, srcAddr, dstAddr, action
| filter (interfaceId = 'eni-05012345abcd' and action = 'REJECT')
| sort @timestamp desc
| limit 5
```
```bash
filter(
action="REJECT" and
dstAddr like   /^(10\.|192\.168\.)/and
srcAddrlike   /^(10\.|192\.168\.)/ and
(
srcAddr = "10.0.0.4" or
dstAddr = "10.0.0.4" or
srcAddr = "10.0.0.5" or
dstAddr = "10.0.0.5" or
srcAddr = "10.0.0.6" or
dstAddr = "10.0.0.6" or
)
)|
stats count(*) as records by srcAddr,dstAddr,dstPort,protocol |
sort records desc |
limit 5
```
## Resource to change to milliseconds
https://repost.aws/knowledge-center/vpc-flow-logs-and-cloudwatch-logs-insights

https://planetcalc.com/7157/
```ruby
fields @timestamp, @message
| fields tomillis(@timestamp) as millis
| display @timestamp, millis, @message
| filter millis > <timestamp_in_milliseconds>
```
```ruby
fields @timestamp, @message, @logStream, @log
| filter @message like /tps\/devices_to_backend/ and @timestamp > 1717338360000 and eventType like 'RuleExecution'
| sort @timestamp asc
| limit 10000
```
