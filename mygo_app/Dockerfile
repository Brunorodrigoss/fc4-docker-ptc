FROM golang:latest AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 go build -ldflags="-s -w" -o server main.go

FROM scratch
WORKDIR /app
COPY --from=builder /app/server .
USER 1001
ENTRYPOINT [ "./server" ]
CMD [ "8080" ]