FROM golang:alpine3.23 as builder

WORKDIR /src

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o dnstt-server ./dnstt-server
RUN CGO_ENABLED=0 GOOS=linux go build -o dnstt-client ./dnstt-client

FROM alpine:3.23 as runtime

COPY --from=builder /src/dnstt-server /usr/local/bin/dnstt-server
COPY --from=builder /src/dnstt-client /usr/local/bin/dnstt-client

ENTRYPOINT [ "dnstt-server" ]
