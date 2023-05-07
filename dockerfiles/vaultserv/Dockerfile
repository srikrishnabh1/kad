FROM golang:1.19.4 AS builder
RUN mkdir /vaultserv
WORKDIR /vaultserv
COPY ./vaultserv ./
RUN rm -rf vendor

RUN go mod download && \
  CGO_ENABLED=0 go build -o vaultserv cmd/main.go

FROM alpine:3.16
RUN apk add --no-cache libc6-compat=1.2.3-r2
WORKDIR /
COPY --from=builder ./vaultserv/vaultserv ./vaultserv

USER 65532:65532
ENTRYPOINT ["./vaultserv"]
