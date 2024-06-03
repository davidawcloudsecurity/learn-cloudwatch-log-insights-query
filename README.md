# learn-cloudwatch-log-insights-query
How to run sql query for cloudwatch log insights

How to find flow logs that has 10.123.85.100 for ports 8834 and REJECT response
```ruby
fields @timestamp, @message, @logStream, @log
| filter @message like /10\.123\.85\.100/ and @message like /8834/ and @message like /REJECT/
| sort @timestamp desc
| limit 1000
```
## Resource to change to milliseconds
https://planetcalc.com/7157/
```ruby
fields @timestamp, @message
| fields tomillis(@timestamp) as millis
| display @timestamp, millis, @message
| filter millis > <timestamp_in_milliseconds>
```
