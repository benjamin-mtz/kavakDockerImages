FROM node:lts-slim

#* setup shell 
SHELL ["/bin/bash", "-c"]

# Hack required by postgresql

RUN for i in {1..8}; do mkdir -p "/usr/share/man/man$i"; done

#* update and deps
RUN echo "deb http://ftp.debian.org/debian stretch-backports main" | tee /etc/apt/sources.list.d/backports.list \
    && apt-get update \
    && apt-get install --no-install-recommends -y -t stretch-backports git \
    && apt-get install --no-install-recommends -y \
    gcc zip curl apt-transport-https \
    ca-certificates gnupg-agent software-properties-common \
    lsb-release gnupg unzip jq openssh-server apt-utils\
    build-essential zlib1g-dev libssl-dev libncurses-dev \
    libffi-dev libsqlite3-dev libreadline-dev libbz2-dev \
    postgresql-client

#* installing docker, serverless, awscli, eb-cli, ecs-cli, yarn, angular
RUN curl -fsSL https://get.docker.com -o get-docker.sh \
    && bash get-docker.sh \
    && curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose \
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
    && npm install -g @angular/cli @nrwl/cli

#* CleanUp
RUN for i in {1..8}; do rm -rf "/usr/share/man/man$i"; done

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

#* Update path && env to help logging
ENV addPath=/root/.serverless/bin:/root/.pyenv/versions/3.7.2/bin:/root/.ebcli-virtual-env/executables
ENV PATH=${addPath}:$PATH
ENV SLS_DEBUG=*

#* Checking installed versions
#* this is commented as is only needed
#* to print out installed versions
RUN aws --version \
    && serverless -version \
    && docker --version \
    && eb --version \
    && ecs-cli --version \
    && yarn -v \
    && ng v \
    && node --version \
    && npm -v \
    && docker-compose --version \
    && nx \
    && lsb_release -a \
    && git --version \
    && docker-compose -v

CMD /bin/bash
