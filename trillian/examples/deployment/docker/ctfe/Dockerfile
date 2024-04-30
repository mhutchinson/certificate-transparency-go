FROM golang:1.22.0-bookworm@sha256:925fe3fa28ba428cf67a7947ae838f8a1523117b40e3e6b5106c378e3f97fa29 as build

ARG GOFLAGS=""
ENV GOFLAGS=$GOFLAGS

WORKDIR /build

COPY go.mod .
COPY go.sum .
RUN go mod download
COPY . .

RUN go build ./trillian/ctfe/ct_server

FROM gcr.io/distroless/base-debian12@sha256:d8d01e2d5868f622544543ca0311679bbc2f3fbf7f7bafd11af78a284c479ea3

COPY --from=build /build/ct_server /

ENTRYPOINT ["/ct_server"]
