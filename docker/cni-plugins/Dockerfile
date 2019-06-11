ARG REPO=github.com/containernetworking/plugins

FROM golang AS builder

ARG REPO=github.com/containernetworking/plugins

ADD / /local/git/src/${REPO}
WORKDIR /local/git/src/${REPO}

RUN GOPATH=/local/git ./build_linux.sh

RUN pwd && ls -l /local/git/src/${REPO}/bin/

FROM alpine

WORKDIR /plugins

COPY --from=builder /local/git/src/github.com/containernetworking/plugins/bin/* /plugins/

RUN pwd && ls -l /plugins

VOLUME [ "/etc/cni/bin/" ]

ENTRYPOINT [ "/bin/sh", "-c" ]
CMD [ "cp -f /plugins/* /etc/cni/bin/" ]