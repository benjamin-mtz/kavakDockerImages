FROM node:lts-slim

#* setup shell 
SHELL ["/bin/bash", "-c"]

#* update and deps
RUN apt-get update \
    && apt-get install --no-install-recommends -y \
    gcc zip git curl apt-transport-https \
    ca-certificates gnupg-agent software-properties-common \
    lsb-release gnupg unzip jq openssh-server apt-utils\
    build-essential zlib1g-dev libssl-dev libncurses-dev \
    libffi-dev libsqlite3-dev libreadline-dev libbz2-dev

#* installing docker, serverless, awscli, eb-cli, ecs-cli, yarn, angular
RUN curl -fsSL https://get.docker.com -o get-docker.sh \
    && bash get-docker.sh \
    && apt-get install -y docker-ce-cli containerd.io \
    && curl -o- -L https://slss.io/install > serverless.sh \
    && bash serverless.sh \
    && curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" \
    && unzip -q awscliv2.zip \
    && bash aws/install \
    && git clone https://github.com/aws/aws-elastic-beanstalk-cli-setup.git \
    && echo 'export PATH=/root/.pyenv/versions/3.7.2/bin:$PATH' >> /root/.bashrc \
    && echo 'export PATH="/root/.ebcli-virtual-env/executables:$PATH"' >> ~/.bashrc \
    && bash aws-elastic-beanstalk-cli-setup/scripts/bundled_installer \
    && curl -o /usr/local/bin/ecs-cli https://amazon-ecs-cli.s3.amazonaws.com/ecs-cli-linux-amd64-latest \
    && chmod +x /usr/local/bin/ecs-cli \
    && curl -o- -L https://yarnpkg.com/install.sh > yarnInstall.sh \
    && bash yarnInstall.sh \
    && npm install -g @angular/cli 

#* CleanUp
RUN apt-get clean --dry-run \
    && apt-get autoclean -y \
    && apt-get autoremove -y  \
    && rm -rf /var/lib/apt/lists/* \
    rm /root/.cache/pip/* \
    rm -rf awscliv2.zip \
    rm -rf get-docker.sh \
    rm -rf serverless.sh \
    rm -rf yarnInstall.sh \
    rm -rf aws-elastic-beanstalk-cli-setup


#* Checking installed versions
RUN source /root/.bashrc  \
    && aws --version \
    && serverless -version \
    && docker --version \
    && eb --version \
    && ecs-cli --version \
    && yarn -v \
    && ng v \
    && node --version \
    && npm -v

CMD source /root/.bashrc && /bin/bash