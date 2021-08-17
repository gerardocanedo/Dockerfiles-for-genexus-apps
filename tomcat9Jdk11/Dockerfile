# Default redirect
FROM tomcat:9.0.52-jdk11-openjdk-slim-buster
LABEL MAINTAINER="gcanedo@genexusconsulting.com"

#VM Optimizations
ENV CATALINA_OPTS="$CATALINA_OPTS -XX:+UseStringDeduplication -XX:+OptimizeStringConcat -XX:+UseCompressedOops  -XX:MaxRAMPercentage=80  -XX:InitialRAMPercentage=10 -XX:+PrintFlagsFinal"

# DISABLE JSP mapping. No needed for GX
RUN cat conf/web.xml | tr '\n' '\r' | sed -e 's@<!\-\- The mappings for the JSP servlet \-\->.*<!\-\- The mapping for the SSI servlet@<!\-\- The mapping for the SSI servlet@g'  | tr '\r' '\n' > /tmp/web.tmp
RUN mv /tmp/web.tmp conf/web.xml

# ClickJacking & SAMEORIGIN
RUN sed -i 's@</web\-app>@<filter><filter-name>httpHeaderSecurity</filter-name><filter-class>org.apache.catalina.filters.HttpHeaderSecurityFilter</filter-class><async-supported>true</async-supported><init-param><param-name>antiClickJackingOption</param-name><param-value>SAMEORIGIN</param-value></init-param></filter><filter-mapping><filter-name>httpHeaderSecurity</filter-name><url-pattern>/*</url-pattern><dispatcher>REQUEST</dispatcher></filter-mapping></web-app>@g' conf/web.xml

# disable reload & enable rewrite valve
RUN sed -i "s@<Context>@<Context><Valve className=\"org.apache.catalina.valves.rewrite.RewriteValve\" /> <JarScanner scanClassPath=\"false\" />@g" conf/context.xml
