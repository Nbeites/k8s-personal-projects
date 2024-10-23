# Start from the official Jenkins inbound agent image
FROM jenkins/inbound-agent:latest

# Switch to root to install Docker
USER root

# Install dependencies
RUN apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg

# Install Docker using the official Docker installation script
RUN curl -fsSL https://get.docker.com | sh

# Add Jenkins user to the Docker group to allow running Docker commands
RUN usermod -aG docker jenkins

# Fix the Docker socket permissions inside the container (this should work for most cases)
RUN chmod 666 /var/run/docker.sock

# Clean up to reduce image size
RUN apt-get clean

# Switch back to Jenkins user
USER jenkins