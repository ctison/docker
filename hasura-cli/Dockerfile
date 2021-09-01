# renovate: github-releases hasura/graphql-engine
ARG HASURA_VERSION=v1.3.2

FROM alpine:3.14.2@sha256:e1c082e3d3c45cccac829840a25941e679c25d438cc8412c2fa221cf1a824e6a as base
ARG HASURA_VERSION
RUN wget -qO /usr/local/bin/hasura https://github.com/hasura/graphql-engine/releases/download/"$HASURA_VERSION"/cli-hasura-linux-amd64

FROM ctison/ubuntu@sha256:42db69f85a170927f2629b3da3f990373d094012d1bfe6c5914b4fa60210af12

COPY --from=base /usr/local/bin/hasura /usr/local/bin/hasura
RUN chmod 555 /usr/local/bin/hasura

RUN useradd -mUs /bin/bash hasura
WORKDIR /home/hasura
USER hasura

ENV HASURA_GRAPHQL_ENABLE_TELEMETRY=false
ARG HASURA_VERSION
RUN hasura plugin install --version "$HASURA_VERSION" cli-ext
ENTRYPOINT ["/usr/local/bin/hasura"]
CMD ["--help"]