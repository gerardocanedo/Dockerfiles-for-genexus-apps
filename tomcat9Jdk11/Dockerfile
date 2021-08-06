FROM tomcat:9-jdk11-openjdk-slim-buster
# Default redirect
ARG WELCOME_FILE=index.jsp
LABEL MAINTAINER="gcanedo@genexusconsulting.com"

#VM Optimizations
ENV CATALINA_OPTS="$CATALINA_OPTS -XX:+UseStringDeduplication -XX:+OptimizeStringConcat -XX:+UseCompressedOops -XX:+AlwaysPreTouch -XX:+PrintFlagsFinal -XX:MinRAMPercentage=75 -XX:MaxRAMPercentage=75 -XX:InitialRAMPercentage=75"

# DISABLE JSP mapping. No needed for GX
RUN cat conf/web.xml | tr '\n' '\r' | sed -e 's@<servlet\-mapping>.*<servlet\-name>jsp</servlet\-name>.*</servlet\-mapping>@@g'  | tr '\r' '\n' > /tmp/web.tmp

# DISABLE JSP mapping. No needed for GX
RUN cat /tmp/web.tmp | tr '\n' '\r' | sed -e 's@<servlet>.*<servlet\-class>org\.apache\.jasper\.servlet\.JspServlet</servlet\-class>.*</servlet>@@g'  | tr '\r' '\n' > conf/web.xml

# ClickJacking & SAMEORIGIN
RUN sed -i 's@</web\-app>@<filter><filter-name>httpHeaderSecurity</filter-name><filter-class>org.apache.catalina.filters.HttpHeaderSecurityFilter</filter-class><async-supported>true</async-supported><init-param><param-name>antiClickJackingOption</param-name><param-value>SAMEORIGIN</param-value></init-param></filter><filter-mapping><filter-name>httpHeaderSecurity</filter-name><url-pattern>/*</url-pattern><dispatcher>REQUEST</dispatcher></filter-mapping></web-app>@g' conf/web.xml

# Set a global entry point. It should be a html file.
RUN sed -i "s@<welcome\-file>index.jsp</welcome\-file>@<welcome-file>${WELCOME_FILE}</welcome-file>@g" conf/web.xml
