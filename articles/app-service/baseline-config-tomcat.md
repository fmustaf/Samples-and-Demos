## Tomcat Baseline Configuration On App Services

As you Provision an App Service with Tomcat to host your Java workload (an EAR file or a JAR file), there certain settings that you get out of the box in the server.xm
for Tomcat. For instance if you are have provisioned a Tomcat 10 instance, following configurations will come out of the box.

```
# Licensed to the Apache Software Foundation (ASF) under one or more
# contributor license agreements.  See the NOTICE file distributed with
# this work for additional information regarding copyright ownership.
# The ASF licenses this file to You under the Apache License, Version 2.0
# (the "License"); you may not use this file except in compliance with
# the License.  You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

#
# List of comma-separated packages that start with or equal this string
# will cause a security exception to be thrown when
# passed to checkPackageAccess unless the
# corresponding RuntimePermission ("accessClassInPackage."+package) has
# been granted.
package.access=sun.,org.apache.catalina.,org.apache.coyote.,org.apache.jasper.,org.apache.tomcat.
#
# List of comma-separated packages that start with or equal this string
# will cause a security exception to be thrown when
# passed to checkPackageDefinition unless the
# corresponding RuntimePermission ("defineClassInPackage."+package) has
# been granted.
#
# by default, no packages are restricted for definition, and none of
# the class loaders supplied with the JDK call checkPackageDefinition.
#
package.definition=sun.,java.,org.apache.catalina.,org.apache.coyote.,\
org.apache.jasper.,org.apache.naming.,org.apache.tomcat.

#
#
# List of comma-separated paths defining the contents of the "common"
# classloader. Prefixes should be used to define what is the repository type.
# Path may be relative to the CATALINA_HOME or CATALINA_BASE path or absolute.
# If left as blank,the JVM system loader will be used as Catalina's "common"
# loader.
# Examples:
#     "foo": Add this folder as a class repository
#     "foo/*.jar": Add all the JARs of the specified folder as class
#                  repositories
#     "foo/bar.jar": Add bar.jar as a class repository
#
# Note: Values are enclosed in double quotes ("...") in case either the
#       ${catalina.base} path or the ${catalina.home} path contains a comma.
#       Because double quotes are used for quoting, the double quote character
#       may not appear in a path.
# AppService:
#       These entries added to loader : "/home/tomcat/lib","/home/tomcat/lib/*.jar"
common.loader="${catalina.base}/lib","${catalina.base}/lib/*.jar","${catalina.home}/lib","${catalina.home}/lib/*.jar","/home/tomcat/lib","/home/tomcat/lib/*.jar","/home/site/libs","/home/site/libs/*.jar","${catalina.base}/appservice/lib/*.jar"

#
# List of comma-separated paths defining the contents of the "server"
# classloader. Prefixes should be used to define what is the repository type.
# Path may be relative to the CATALINA_HOME or CATALINA_BASE path or absolute.
# If left as blank, the "common" loader will be used as Catalina's "server"
# loader.
# Examples:
#     "foo": Add this folder as a class repository
#     "foo/*.jar": Add all the JARs of the specified folder as class
#                  repositories
#     "foo/bar.jar": Add bar.jar as a class repository
#
# Note: Values may be enclosed in double quotes ("...") in case either the
#       ${catalina.base} path or the ${catalina.home} path contains a comma.
#       Because double quotes are used for quoting, the double quote character
#       may not appear in a path.
server.loader=

#
# List of comma-separated paths defining the contents of the "shared"
# classloader. Prefixes should be used to define what is the repository type.
# Path may be relative to the CATALINA_BASE path or absolute. If left as blank,
# the "common" loader will be used as Catalina's "shared" loader.
# Examples:
#     "foo": Add this folder as a class repository
#     "foo/*.jar": Add all the JARs of the specified folder as class
#                  repositories
#     "foo/bar.jar": Add bar.jar as a class repository
# Please note that for single jars, e.g. bar.jar, you need the URL form
# starting with file:.
#
# Note: Values may be enclosed in double quotes ("...") in case either the
#       ${catalina.base} path or the ${catalina.home} path contains a comma.
#       Because double quotes are used for quoting, the double quote character
#       may not appear in a path.
shared.loader=

# Default list of JAR files that should not be scanned using the JarScanner
# functionality. This is typically used to scan JARs for configuration
# information. JARs that do not contain such information may be excluded from
# the scan to speed up the scanning process. This is the default list. JARs on
# this list are excluded from all scans. The list must be a comma separated list
# of JAR file names.
# The list of JARs to skip may be over-ridden at a Context level for individual
# scan types by configuring a JarScanner with a nested JarScanFilter.
# The JARs listed below include:
# - Tomcat Bootstrap JARs
# - Tomcat API JARs
# - Catalina JARs
# - Jasper JARs
# - Tomcat JARs
# - Common non-Tomcat JARs
# - Test JARs (JUnit, Cobertura and dependencies)
tomcat.util.scan.StandardJarScanFilter.jarsToSkip=\
azure.appservice.jar, \
azure.appservice.easyauth.jar, \
annotations-api.jar,\
ant-junit*.jar,\
ant-launcher.jar,\
ant.jar,\
asm-*.jar,\
aspectj*.jar,\
bootstrap.jar,\
catalina-ant.jar,\
catalina-ha.jar,\
catalina-ssi.jar,\
catalina-storeconfig.jar,\
catalina-tribes.jar,\
catalina.jar,\
cglib-*.jar,\
cobertura-*.jar,\
commons-beanutils*.jar,\
commons-codec*.jar,\
commons-collections*.jar,\
commons-daemon.jar,\
commons-dbcp*.jar,\
commons-digester*.jar,\
commons-fileupload*.jar,\
commons-httpclient*.jar,\
commons-io*.jar,\
commons-lang*.jar,\
commons-logging*.jar,\
commons-math*.jar,\
commons-pool*.jar,\
derby-*.jar,\
dom4j-*.jar,\
easymock-*.jar,\
ecj-*.jar,\
el-api.jar,\
geronimo-spec-jaxrpc*.jar,\
h2*.jar,\
hamcrest-*.jar,\
hibernate*.jar,\
httpclient*.jar,\
icu4j-*.jar,\
jakartaee-migration-*.jar,\
jasper-el.jar,\
jasper.jar,\
jaspic-api.jar,\
jaxb-*.jar,\
jaxen-*.jar,\
jdom-*.jar,\
jetty-*.jar,\
jmx-tools.jar,\
jmx.jar,\
jsp-api.jar,\
jstl.jar,\
jta*.jar,\
junit-*.jar,\
junit.jar,\
log4j*.jar,\
mail*.jar,\
objenesis-*.jar,\
oraclepki.jar,\
oro-*.jar,\
servlet-api-*.jar,\
servlet-api.jar,\
slf4j*.jar,\
taglibs-standard-spec-*.jar,\
tagsoup-*.jar,\
tomcat-api.jar,\
tomcat-coyote.jar,\
tomcat-dbcp.jar,\
tomcat-i18n-*.jar,\
tomcat-jdbc.jar,\
tomcat-jni.jar,\
tomcat-juli-adapters.jar,\
tomcat-juli.jar,\
tomcat-util-scan.jar,\
tomcat-util.jar,\
tomcat-websocket.jar,\
tools.jar,\
websocket-api.jar,\
wsdl4j*.jar,\
xercesImpl.jar,\
xml-apis.jar,\
xmlParserAPIs-*.jar,\
xmlParserAPIs.jar,\
xom-*.jar

# Default list of JAR files that should be scanned that overrides the default
# jarsToSkip list above. This is typically used to include a specific JAR that
# has been excluded by a broad file name pattern in the jarsToSkip list.
# The list of JARs to scan may be over-ridden at a Context level for individual
# scan types by configuring a JarScanner with a nested JarScanFilter.
tomcat.util.scan.StandardJarScanFilter.jarsToScan=\
log4j-taglib*.jar,\
log4j-web*.jar,\
log4javascript*.jar,\
slf4j-taglib*.jar

# String cache configuration.
tomcat.util.buf.StringCache.byte.enabled=true
#tomcat.util.buf.StringCache.char.enabled=true
#tomcat.util.buf.StringCache.trainThreshold=500000
#tomcat.util.buf.StringCache.cacheSize=5000
```

Additionally, there are certain transformationss that are further applied on top of the server.xml for Tomcat distribution upon start

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
