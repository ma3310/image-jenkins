# docker build -t ma3310/jenkins:lts-jdk11-docker .
# If build image hehind proxy add below command line option:
#   --build-arg JAVA_TOOL_OPTIONS="-Dhttps.proxyHost=PROXY_HOST -Dhttps.proxyPort=PROXY_PORT -Dhttp.nonProxyHosts=localhost|127.*|[::1]"
FROM jenkins/jenkins:lts-jdk11
USER root
RUN apt-get update && apt-get install -y apt-transport-https \
  ca-certificates curl gnupg2 \
  software-properties-common
RUN curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add -
RUN apt-key fingerprint 0EBFCD88
RUN add-apt-repository \
  "deb [arch=amd64] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y docker-ce-cli
USER jenkins

# receive and export JAVA_TOOL_OPTIONS from Docker build command
#ARG JAVA_TOOL_OPTIONS
RUN jenkins-plugin-cli --plugins "blueocean:1.25.0 docker-workflow:1.26"
