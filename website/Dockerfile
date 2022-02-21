FROM golang:1.16.7-alpine AS builder
WORKDIR /opt/web/
COPY go.mod go.sum ./
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -ldflags="-w -s" -a -installsuffix cgo -o /go/bin/cinema-website ./cmd/web

FROM alpine:3.15.0
WORKDIR /opt/web/
COPY --from=builder /go/bin/cinema-website cinema-website
COPY ./ui ui
ENTRYPOINT ["./cinema-website"]
