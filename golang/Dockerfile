FROM golang:1.16.4@sha256:6f0b0a314b158ff6caf8f12d7f6f3a966500ec6afb533e986eca7375e2f7560f

SHELL [ "/bin/bash", "--norc", "--noprofile", "-euxo", "pipefail", "-O", "nullglob", "-c" ]
ENV LANG C.UTF-8
ARG GO111MODULE=on

ARG DEBIAN_FRONTEND=noninteractive
# hadolint ignore=DL3008
RUN apt-get update && \
  apt-get install --no-install-recommends -y ca-certificates curl && \
  rm -rf -- /var/lib/apt/lists/

# renovate: github-releases goreleaser/goreleaser
ARG GORELEASER_VERSION='v0.165.0'
RUN curl -LO https://github.com/goreleaser/goreleaser/releases/download/"$GORELEASER_VERSION"/goreleaser_Linux_x86_64.tar.gz && \
  tar --no-same-{o,p} -C /usr/local/bin/ -xf goreleaser_Linux_x86_64.tar.gz goreleaser && \
  chmod 500 /usr/local/bin/goreleaser && \
  rm goreleaser_Linux_x86_64.tar.gz

# renovate: github-releases golangci/golangci-lint
ARG GOLANGCI_VERSION='v1.40.1'
RUN curl -LO https://github.com/golangci/golangci-lint/releases/download/"$GOLANGCI_VERSION"/golangci-lint-"${GOLANGCI_VERSION#v}"-linux-amd64.tar.gz && \
  tar --no-same-{o,p} -C /usr/local/bin/ --strip=1 -xf golangci-lint-"${GOLANGCI_VERSION#v}"-linux-amd64.tar.gz golangci-lint-"${GOLANGCI_VERSION#v}"-linux-amd64/golangci-lint && \
  chmod 500 /usr/local/bin/golangci-lint && \
  rm golangci-lint-"${GOLANGCI_VERSION#v}"-linux-amd64.tar.gz