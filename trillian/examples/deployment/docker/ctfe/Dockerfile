FROM golang:1.22.3-bookworm@sha256:6d71b7c3f884e7b9552bffa852d938315ecca843dcc75a86ee7000567da0923d as build

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
