FROM tomcat:8.0-alpine
LABEL maintainer="zippyops@gmail.com"
RUN rm -rf /usr/local/tomcat/webapps/*
copy ./target/newapp-0.0.1-SNAPSHOT.war /usr/local/tomcat/webapps/
EXPOSE 8080
CMD ["catalina.sh", "run"]
