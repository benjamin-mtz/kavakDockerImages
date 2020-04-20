FROM node:lts-slim
RUN apt-get update \
    && apt-get install --no-install-recommends zip git jq openssh-client curl -y \
    && apt-get autoremove -y \
    && apt-get clean --dry-run \
    && apt-get clean --dry-run \
    && rm -rf /var/lib/apt-get/lists/*

RUN npm install -g @angular/cli \
    && ng version
CMD ["/bin/bash"]
