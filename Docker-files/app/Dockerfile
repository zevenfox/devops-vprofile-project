FROM openjdk:11 AS BUILD_IMAGE
RUN apt update && apt install maven -y
RUN git clone https://github.com/zevenfox/devops-vprofile-project.git vprofile-project
RUN cd vprofile-project && git checkout docker &&  mvn install 

FROM tomcat:9-jre11
LABEL "Project"="Vprofile"
LABEL "Author"="Imran"
RUN rm -rf /usr/local/tomcat/webapps/*
COPY --from=BUILD_IMAGE vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

EXPOSE 8080
CMD ["catalina.sh", "run"]
# # Stage 1: Build image with Maven
# FROM openjdk:11 AS BUILD_IMAGE
# RUN apt update && apt install maven -y
# WORKDIR /app
# RUN git clone https://github.com/zevenfox/devops-vprofile-project.git
# WORKDIR /app/devops-vprofile-project
# RUN git checkout docker && mvn install

# # Stage 2: Copy the WAR file to Tomcat
# FROM tomcat:9-jre11
# LABEL "Project"="Vprofile"
# LABEL "Author"="zevenfox"
# COPY --from=BUILD_IMAGE /app/devops-vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# # Clear default Tomcat webapps
# RUN rm -rf /usr/local/tomcat/webapps/*

# EXPOSE 8080
# CMD ["catalina.sh", "run"]
