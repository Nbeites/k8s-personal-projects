FROM jenkins/inbound-agent:latest

# Switch to root user to install Docker and its dependencies
USER root

# Install Docker dependencies
RUN apt-get update && \
    apt-get install -y apt-transport-https ca-certificates curl gnupg2 lsb-release software-properties-common && \
    curl -fsSL https://download.docker.com/linux/debian/gpg | apt-key add - && \
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) stable" && \
    apt-get update && \
    apt-get install -y docker-ce docker-ce-cli containerd.io && \
    apt-get clean

# Add Jenkins user to the docker group to allow running Docker commands without sudo
RUN usermod -aG docker jenkins

# Clean up unused packages and caches
RUN apt-get autoremove -y && apt-get clean

# Switch back to Jenkins user
USER jenkins

# Enable Docker-in-Docker by mounting the Docker socket at runtime
VOLUME /var/run/docker.sock