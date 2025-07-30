FROM ubuntu:22.04

RUN apt-get update && \
    apt-get install -y curl gnupg2 openjdk-17-jdk git wget && \
    mkdir -p /usr/share/jenkins && \
    wget https://get.jenkins.io/war-stable/latest/jenkins.war -O /usr/share/jenkins/jenkins.war && \
    apt-get clean

EXPOSE 8080 50000

ENV JENKINS_HOME=/var/lib/jenkins

CMD ["java", "-jar", "/usr/share/jenkins/jenkins.war"]

