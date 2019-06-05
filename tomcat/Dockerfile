# Set the base image to Ubuntu
FROM ubuntu:14.04

# Updating repositories
RUN apt-get update && apt-get install -y wget

# Fetching tarball for jdk-8
RUN wget --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u5-b13/jdk-8u5-linux-x64.tar.gz

# Creating directory for jdk to install
RUN mkdir /opt/jdk && tar -zxf jdk-8u5-linux-x64.tar.gz -C /opt/jdk

# Updating to default java version
RUN update-alternatives --install /usr/bin/java java /opt/jdk/jdk1.8.0_05/bin/java 100 && update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk1.8.0_05/bin/javac 100

# Fetching tarball for tomcat6
RUN wget http://mirror.fibergrid.in/apache/tomcat/tomcat-6/v6.0.53/bin/apache-tomcat-6.0.53.tar.gz

# Untaring tomcat to the appropriate directory
RUN mkdir /usr/local/tomcat && tar xvzf apache-tomcat-6.0.53.tar.gz -C /usr/local/tomcat

# Exporting variables to enviornment
ENV CATALINA_BASE /usr/local/tomcat/apache-tomcat-6.0.53

ENV CATALINA_HOME /usr/local/tomcat/apache-tomcat-6.0.53

ENV PATH $CATALINA_HOME/bin:$PATH

ENV CATALINA_TMPDIR /usr/local/tomcat/apache-tomcat-6.0.53/temp

ENV JRE_HOME /opt/jdk/jdk1.8.0_05

ENV JAVA_HOME /opt/jdk/jdk1.8.0_05

ENV CLASSPATH /usr/local/tomcat/apache-tomcat-6.0.53/bin/bootstrap.jar

# Creating environment variable for mysql_ip
ENV mysql_ip ${mysql_ip}

# Defining build time arguments
ARG version

# Deploying application to tomcat
RUN wget -O /usr/local/tomcat/apache-tomcat-6.0.53/webapps/evailApp.war https://s3.amazonaws.com/downloads.wavemaker.com/wavemaker-ops/ansibleTomcat/$version/evailApp.war

#Exposing ports
EXPOSE 8080

# Starting tomcat
CMD ["catalina.sh", "run"]

