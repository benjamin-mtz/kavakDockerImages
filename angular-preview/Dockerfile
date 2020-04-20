FROM node:lts-slim
RUN apt update \
    && aptt install --no-install-recommends zip git jq openssh-client curl -y \
    && apt autoremove \
    && apt-get clean --dry-run \
    && rm -rf /var/lib/apt/lists/*

RUN npm install -g @angular/cli \
    && ng version
CMD ["/bin/bash"]
