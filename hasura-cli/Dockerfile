# renovate: github-releases hasura/graphql-engine
ARG HASURA_VERSION=v1.3.2

FROM alpine:3.14.0@sha256:3f1b0108cd342368e0e7884a7e30a57430bd472a050c582f9e56ace511a086f1 as base
ARG HASURA_VERSION
RUN wget -qO /usr/local/bin/hasura https://github.com/hasura/graphql-engine/releases/download/"$HASURA_VERSION"/cli-hasura-linux-amd64

FROM ctison/ubuntu@sha256:4031298efd02eb53d038c3c96a57726aaea8ba66a5cbe14159cbeb97f9fa5007

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