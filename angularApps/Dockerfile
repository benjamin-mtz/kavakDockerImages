FROM node:lts-slim
RUN apt-get update \
    && apt-get install --no-install-recommends zip git jq openssh-client -y \
    && apt-get clean --dry-run \
    && rm -rf /var/lib/apt/lists/*

RUN npm install -g @angular/cli \
    && ng version
CMD ["/bin/bash"]
