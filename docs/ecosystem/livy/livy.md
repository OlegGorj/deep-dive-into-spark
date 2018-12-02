# Livy

## Overview

### Create a YARN Session
![create a YARN session](livy-create-session.png)

### Module Relationship

![module relationship](livy-module-relationship.png)

### Execute Codes

![execute codes](livy-repl-execute-code.png)

## Modules

### livy-api


### livy-client-http


### livy-server

![livy-server classes](livy-server-classes.png)

### livy-rsc


### livy-repl

![livy-repl classes](livy-repl-classes.png)

### livy-core

## Misc

### Logging

1. `livy-<user>-server.out`
2. `yyyy_mm_dd.request.log`. WebServer uses `org.eclipse.jetty.server.handler.RequestLogHandler`, 
in turn uses `org.eclipse.jetty.server.NCSARequestLog`.
3. `livy.log`. configured via `$LIVY_CONF_DIR/log4j.properties`

## References
* https://github.com/spark-jobserver/spark-jobserver
* Using Apache Spark to serve real time web services queries. http://stackoverflow.com/questions/30653571/using-apache-spark-to-serve-real-time-web-services-queries
* http://www.slideshare.net/SparkSummit/productionizing-spark-and-the-rest-job-server-evan-chan
