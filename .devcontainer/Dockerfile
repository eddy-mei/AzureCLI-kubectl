# You can pick any Debian/Ubuntu-based image. 😊
FROM mcr.microsoft.com/devcontainers/base:bullseye

# [Option] Install zsh
ARG INSTALL_ZSH="true"
# [Option] Upgrade OS packages to their latest versions
ARG UPGRADE_PACKAGES="false"

# Install needed packages and setup non-root user. Use a separate RUN statement to add your own dependencies.
ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID
COPY library-scripts/*.sh /tmp/library-scripts/
RUN bash /tmp/library-scripts/common-debian.sh "${INSTALL_ZSH}" "${USERNAME}" "${USER_UID}" "${USER_GID}" "${UPGRADE_PACKAGES}" "true" "true" \
    # Install the Azure CLI
    && bash /tmp/library-scripts/azcli-debian.sh \
    # Clean up
    && apt-get clean -y && rm -rf /var/lib/apt/lists/* /tmp/library-scripts

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>

#RUN sudo curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
#RUN sudo curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256" \
#    && echo "$(cat kubectl.sha256)  kubectl" | sha256sum --check

#RUN sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

#RUN sudo chmod +x kubectl 
#RUN sudo mkdir -p ~/.local/bin 
#RUN sudo mv ./kubectl ~/.local/bin/kubectl

RUN cd ~ \
    && sudo wget https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-395.0.0-linux-arm.tar.gz \
    && tar -zxvf google-cloud-cli-395.0.0-linux-arm.tar.gz
    
RUN apt update 
RUN apt install -y nodejs npm