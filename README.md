logstash-log4j2
===============

Log4j2 plugin for logstash.

Get the plugin
----
Download the latest release at: https://github.com/jurmous/logstash-log4j2/releases and unzip it.

Setup log4j2
------------

Add the included `Log4jExtension-0.2.0.jar` to your classpath. (Or your own maven repository)

Set log4j2.xml in your project
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration packages="jurmous.log4j">
    <Appenders>
        <Socket name="A1" host="localHost" port="7000">
            <SerializedLogEventLayout />
        </Socket>
    </Appenders>
    <Loggers>
        <Root level="debug">
            <AppenderRef ref="A1"/>
        </Root>
    </Loggers>
</Configuration>
```

Setup logstash
-----

```
input {
  log4j2 {
    port => 7000
    mode => "server"
  }
}

output {
  stdout { codec => rubydebug }
}
```

Run logstash with the plugin
-------------

Run from your logstash install directory `./bin/logstash --pluginpath PATH_TO_PLUGIN -f YOUR_CONF.conf`


Related project
--------------
https://github.com/jurmous/log4jextensions - Source of the serialization jar.