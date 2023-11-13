# Use golang:1.21 as the base image for building
FROM golang:1.21 AS builder

# Set the working directory
WORKDIR /app

# Copy the Go module files to the working directory
COPY go.mod go.sum ./

# Download and install Go dependencies
RUN go mod download

# Copy the source code to the working directory
COPY . .

# Build the Go application
RUN CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o myapp .

# Use gcr.io/distroless/static-debian12:latest-amd64 as the base image for runtime
FROM gcr.io/distroless/static-debian12:latest-amd64

# Copy the built binary from the builder stage
COPY --from=builder /app/myapp /

# Set the entry point for the application
ENTRYPOINT ["/myapp"]
