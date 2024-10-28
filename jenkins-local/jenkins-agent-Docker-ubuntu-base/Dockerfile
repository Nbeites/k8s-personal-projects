# This was tried, the Dockefile builds but does not work on any deployment
# of jenkins agent, here in case of need as an example of base ubuntu image

# This example is used to install jenkins agent in ubuntu base,
# but can be adapted to be used as clean ubuntu image :) by removing
# jenkins agent related stuff

FROM ubuntu:20.04

# Install dependencies and tools for Docker installation
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    nano \
    software-properties-common

# Add Docker’s official GPG key
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -

# Set up the stable Docker repository
RUN add-apt-repository \
   "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# Install Docker
RUN apt-get update && apt-get install -y docker-ce docker-ce-cli containerd.io

# Install Jenkins inbound agent dependencies
RUN apt-get install -y openjdk-17-jdk git

# Create Jenkins user
RUN useradd -m jenkins

# Download the Jenkins agent jar as root
USER root
RUN mkdir -p /usr/share/jenkins && \
    curl --create-dirs -sSLo /usr/share/jenkins/agent.jar https://repo.jenkins-ci.org/public/org/jenkins-ci/main/remoting/4.10/remoting-4.10.jar && \
    chmod 755 /usr/share/jenkins/agent.jar

# Switch back to Jenkins user
USER jenkins
ENV HOME=/home/jenkins


# Set up the Jenkins agent entrypoint
ENTRYPOINT ["java", "-jar", "/usr/share/jenkins/agent.jar"]