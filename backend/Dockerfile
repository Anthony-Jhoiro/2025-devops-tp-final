# Step 1: Build the Go application
FROM golang:1.23 AS builder

WORKDIR /app

COPY ./go.mod ./go.sum ./

RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build -o server ./cmd/server/main.go

# Step 2 : Create a lightweight runtime image
FROM scratch

WORKDIR /app

COPY --from=builder /app/server .

EXPOSE 8080

ENTRYPOINT ["./server"]