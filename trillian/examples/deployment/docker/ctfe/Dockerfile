FROM golang:1.22.2-bookworm@sha256:48b942a5a9803fafeb748f1a9c6edeb71e06653bb4df25f63f909151e15e9618 as build

ARG GOFLAGS=""
ENV GOFLAGS=$GOFLAGS

WORKDIR /build

COPY go.mod .
COPY go.sum .
RUN go mod download
COPY . .

RUN go build ./trillian/ctfe/ct_server

FROM gcr.io/distroless/base-debian12@sha256:2102ce121ff1448316b93c5f347118a8e604f5ba7ec9dd7a5c2d8b0eac2941fe

COPY --from=build /build/ct_server /

ENTRYPOINT ["/ct_server"]
