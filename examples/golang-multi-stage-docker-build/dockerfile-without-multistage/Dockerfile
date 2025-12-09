#############################################
# BASE IMAGE (BUILD STAGE)
#############################################

FROM ubuntu AS build

# Install Go compiler
RUN apt-get update && apt-get install -y golang-go

# Disable Go modules (optional for simple projects)
ENV GO111MODULE=off

# Copy source code into the build container
COPY . .

# Build the Go program as a static binary (required for distroless)
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /app .


#############################################
# FINAL IMAGE (DISTROLESS — Secure & Minimal)
#############################################

FROM gcr.io/distroless/base-debian12

# Copy the compiled binary from the build stage
COPY --from=build /app /app

# Run the Go executable
ENTRYPOINT ["/app"]


