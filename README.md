# learn-cloudwatch-log-insights-query
How to run sql query for cloudwatch log insights

How to find flow logs that has 10.123.85.100 for ports 8834 and REJECT response
```ruby
fields @timestamp, @message, @logStream, @log
| filter @message like /10\.123\.85\.100/ and @message like /8834/ and @message like /REJECT/
| sort @timestamp desc
| limit 1000
```
29 May 2024, 00:00:00: 1716940800000 milliseconds

https://chatgpt.com/c/f2a030a6-e0e0-4e13-a7e8-c77dfa306c2d
```ruby
fields @timestamp, @message
| fields tomillis(@timestamp) as millis
| display @timestamp, millis, @message
| filter millis > <timestamp_in_milliseconds>
```
