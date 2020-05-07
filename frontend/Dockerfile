FROM alpine:latest
RUN apk add --no-cache curl zip git jq coreutils openssh-client nodejs npm

RUN node --version && \
    npm --version
CMD ["/bin/sh"]
