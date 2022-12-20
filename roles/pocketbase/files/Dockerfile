FROM alpine:latest

ARG PB_VERSION=0.10.2

RUN apk add --no-cache \
    unzip \
    ca-certificates

# download and unzip PocketBase
ADD https://github.com/pocketbase/pocketbase/releases/download/v${PB_VERSION}/pocketbase_${PB_VERSION}_linux_arm64.zip /tmp/pb.zip
RUN unzip /tmp/pb.zip -d /pb/

EXPOSE 12000

# start PocketBase
CMD ["/pb/pocketbase", "serve", "--http=0.0.0.0:12000"]