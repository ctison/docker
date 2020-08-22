ARG HASURA_VERSION=v1.3.0

FROM alpine:3.12.0@sha256:a15790640a6690aa1730c38cf0a440e2aa44aaca9b0e8931a9f2b0d7cc90fd65 as base
ARG HASURA_VERSION
RUN wget -qO /usr/local/bin/hasura https://github.com/hasura/graphql-engine/releases/download/"$HASURA_VERSION"/cli-hasura-linux-amd64

FROM ctison/ubuntu@sha256:26c99d156f9852580a3454ab170ee15803ee677430c6d0dd91085741c63054ba

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