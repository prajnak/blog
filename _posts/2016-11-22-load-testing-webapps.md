---
published: false
---
# Intro

## Assumptions 

You've just deployed your web application to a cloud provider or
have it running on your local machine and would like to find out how well it
performs under load.

## What is Load?

Load refers to resource usage by the machine hosting your web application. CPU,
memory, database access and a ton of things come into play as a web server under
load has concurrent users hitting various routes in your application.

## Common Bottlenecks

Creating a webserver that can handle atleast 1000 concurrent users at a time is
a solved problem. The following bottlenecks can be taken care of by using an
industry standard webserver like Nginx

1. Static asset serving - gzipping, caching
2. load balancing

So, if you want to solve the most common bottlenecks associated with web hosting, use nginx

## Fuck nginx, I want to know how bad my web framework's http server really is

Now that we're here, let's see how we can stress test our web server. We'll use this tool called [Siege](https://github.com/JoeDog/siege). From their website,

`Siege was written for both web developers and web systems admin- istrators. It allows those individuals to test their programs and their systems under duress. As a web professional, you are responsible for the intregrity of your product, yet you have no control over who accesses it. Traffic spikes can occur at any moment. How do you know if you're prepared?`

### Install Siege

There's no hand-holding here as the instructions in the
[INSTALL](https://github.com/JoeDog/siege/blob/master/INSTALL) document are
pretty thorough.

Just make sure you're running siege on a machine that's not your server.

### Using siege 

```bash 
siege -c 100 <url that accepts GET or POST requests> 
```

`Ctrl-C` when you're satisfied that your web server and database has suffered enough under siege's
attempts. Here is some sample output from Siege:

```
HTTP/1.1 200     0.08 secs:   10299 bytes ==> GET  /css/milligram.css
HTTP/1.1 200     0.19 secs:  130947 bytes ==> GET  /mapbox-gl-js/v0.27.0/mapbox-gl.js
HTTP/1.1 200     0.15 secs:    1010 bytes ==> GET  /css?family=Roboto:300,300italic,700,700italic
HTTP/1.1 200     0.07 secs:    2592 bytes ==> GET  /
^C
Lifting the server siege...
Transactions:		         547 hits
Availability:		      100.00 %
Elapsed time:		       28.33 secs
Data transferred:	       12.90 MB
Response time:		        0.90 secs
Transaction rate:	       19.31 trans/sec
Throughput:		        0.46 MB/sec
Concurrency:		       17.30
Successful transactions:         547
Failed transactions:	           0
Longest transaction:	       11.14
Shortest transaction:	        0.06

```

## Conclusion
Hope this helps you create more resilient web infrastructure.

