# Build stage
FROM golang:1.22.12-alpine3.21 AS builder

WORKDIR /app

COPY go.mod .

RUN go mod download

COPY . .

ENV CGO_ENABLED=0 GOOS=linux GOARCH=amd64

# Build
RUN go build -o main ./main.go

# Final stage

FROM alpine:3.22

# RUN addgroup -S srvgrp && adduser -S srvusr -G srvgrp 

WORKDIR /server

COPY --from=builder /app/main .
COPY --from=builder /app/static ./static

EXPOSE 8080

# USER srvusr

ENTRYPOINT ["./main"]