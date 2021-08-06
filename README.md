# Dockerfiles-for-genexus-apps
Dockerfiles images for genexus web applications


# tomcat9Jdk11
Dockerfile based on tomcat:9-jdk11-openjdk-slim-buster
WELCOME_FILE ARG redirects to the index page

publishing process:

docker build -t tomcat9_jdk11_for_genexus:latest . ;
docker tag tomcat9_jdk11_for_genexus:latest gerardocanedo/tomcat9_jdk11_for_genexus ;
docker push gerardocanedo/tomcat9_jdk11_for_genexus

Review:
-XX:+AlwaysPreTouch -XX:MinRAMPercentage=50 -XX:MaxRAMPercentage=70 -XX:InitialRAMPercentage=50