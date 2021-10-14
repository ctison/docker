FROM golang:1.17.2@sha256:cf615c1499e8bc2cf00696ba234cddd47fdb8d9a3b37b7c35726e46ee4ae08cc

SHELL [ "/bin/bash", "--norc", "--noprofile", "-euxo", "pipefail", "-O", "nullglob", "-c" ]
ENV LANG C.UTF-8
ARG GO111MODULE=on

ARG DEBIAN_FRONTEND=noninteractive
# hadolint ignore=DL3008
RUN apt-get update && \
  apt-get install --no-install-recommends -y ca-certificates curl && \
  rm -rf -- /var/lib/apt/lists/

# renovate: github-releases goreleaser/goreleaser
ARG GORELEASER_VERSION='v0.182.1'
RUN curl -LO https://github.com/goreleaser/goreleaser/releases/download/"$GORELEASER_VERSION"/goreleaser_Linux_x86_64.tar.gz && \
  tar --no-same-{o,p} -C /usr/local/bin/ -xf goreleaser_Linux_x86_64.tar.gz goreleaser && \
  chmod 500 /usr/local/bin/goreleaser && \
  rm goreleaser_Linux_x86_64.tar.gz

# renovate: github-releases golangci/golangci-lint
ARG GOLANGCI_VERSION='v1.42.1'
RUN curl -LO https://github.com/golangci/golangci-lint/releases/download/"$GOLANGCI_VERSION"/golangci-lint-"${GOLANGCI_VERSION#v}"-linux-amd64.tar.gz && \
  tar --no-same-{o,p} -C /usr/local/bin/ --strip=1 -xf golangci-lint-"${GOLANGCI_VERSION#v}"-linux-amd64.tar.gz golangci-lint-"${GOLANGCI_VERSION#v}"-linux-amd64/golangci-lint && \
  chmod 500 /usr/local/bin/golangci-lint && \
  rm golangci-lint-"${GOLANGCI_VERSION#v}"-linux-amd64.tar.gz