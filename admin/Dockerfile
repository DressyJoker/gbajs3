# first stage - builder
FROM golang:alpine AS builder
WORKDIR /app/
COPY . /app/
RUN apk update && apk add make
ENV GO111MODULE=on
RUN go mod download
RUN make build

# second stage
FROM alpine:latest

LABEL org.opencontainers.image.source https://github.com/thenick775/gbajs3

WORKDIR /app/
COPY --from=builder /app/build/goadmin .
COPY --from=builder /app/html/ ./html
RUN mkdir ./logs
CMD ["./goadmin"]
