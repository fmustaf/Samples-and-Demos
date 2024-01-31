## Tomcat Baseline Configuration On App Services

As you provision an App Service with Tomcat to host your Java workload (an WAR file or a JAR file), there are certain settings that you get out of the box for Tomcat configuration. You can refer to the [Official Apcache Tomcat Documentation](https://tomcat.apache.org/) for detailed infoirmation, including the default configuration for Tomcat Web Server.

Additionally, there are certain transformationss that are further applied on top of the server.xml for Tomcat distribution upon start.

### Connector

``` 
<Connector port="${port.http}" address="127.0.0.1" maxHttpHeaderSize="16384" compression="on" URIEncoding="UTF-8" connectionTimeout="${site.connectionTimeout}" maxThreads="${catalina.maxThreads}" maxConnections="${catalina.maxConnections}" protocol="HTTP/1.1" redirectPort="8443"/>
 ```
* maxHttpHeaderSize to 16384
* URIEncoding to UTF-8
* conectionTimeout to (WEBSITE_TOMCAT_CONNECTION_TIMEOUT, default 240000)
* maxThreads to (WEBSITE_CATALINA_MAXTHREADS, default 200)
* maxConnections to (WEBSITE_CATALINA_MAXCONNECTIONS, default 10000)
 
> **NOTE**: The conectionTimeout, maxThreads and maxConnections can be tuned with theseapp settings
 
### Host

```
<Host appBase="${site.appbase}" xmlBase="${site.xmlbase}" unpackWARs="${site.unpackwars}" workDir="${site.tempdir}" errorReportValveClass="com.microsoft.azure.appservice.AppServiceErrorReportValve" name="localhost" autoDeploy="true">
```

* appBase to (AZURE_SITE_APP_BASE, defaults to local WebappsLocalPath)
* xmlBase to (AZURE_SITE_HOME, /site/wwwroot)
* unpackWARs to (AZURE_UNPACK_WARS, default true)
* workDir to (JAVA_TMP_DIR, default TMP)
* errorReportValveClass uses our custom error report valve
 
### Valve

```
<Valve prefix="site_access_log.${catalina.instance.name}" pattern="%h %l %u %t &quot;%r&quot; %s %b %D %{x-arr-log-id}i" directory="${site.logdir}/http/RawLogs" maxDays="${site.logRetentionDays}" className="org.apache.catalina.valves.AccessLogValve" suffix=".txt"/>
 ```
* directory to (AZURE_LOGGING_DIR, default home\logFiles)
* maxDays to (WEBSITE_HTTPLOGGING_RETENTION_DAYS, default 0 [forever] )
 
On Linux, it has all of the same customization, plus:
 
* Adds some error and reporting pages to the valve:
 ```
                <xsl:attribute name="appServiceErrorPage">
                    <xsl:value-of select="'${appService.valves.appServiceErrorPage}'"/>
                </xsl:attribute>
 
                <xsl:attribute name="showReport">
                    <xsl:value-of select="'${catalina.valves.showReport}'"/>
                </xsl:attribute>
                
                <xsl:attribute name="showServerInfo">
                    <xsl:value-of select="'${catalina.valves.showServerInfo}'"/>
                </xsl:attribute>
 ```
* Connector uses the address of the container instead of 127.0.0.1
 
Notably, the latest versions of Tomcat will have these server.xml. (8.5.58 and 9.0.38 onward). Older versions of Tomcat do not use transforms and may have different behavior as a result.
