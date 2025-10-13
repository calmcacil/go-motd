# MOTD - Go Implementation

A Go implementation of MOTD (Message of the Day) that displays system information, service status, and media service statistics.

## Features

- **Fast Execution**: Compiled binary with quick startup time
- **Concurrent HTTP Requests**: Uses Go's native HTTP client with connection pooling
- **Low Memory Footprint**: Efficient memory management
- **Cross-Platform**: Can be compiled for different architectures

## Build

All build outputs are placed in the `bin/` directory:

```bash
# Build regular binary
make build
# Output: bin/motd

# Build optimized binary (recommended)
make build-optimized
# Output: bin/motd
```

Or using Go directly:

```bash
# Regular build
mkdir -p bin && go build -o bin/motd main.go

# Optimized build (smaller binary)
mkdir -p bin && go build -ldflags="-s -w" -o bin/motd main.go
```

The `-s -w` flags strip debug information and symbol tables, reducing binary size.

## Usage

```bash
./motd [OPTIONS]

Options:
  -h    Show this help message
  -v    Show version information
  -V    Show optional dependency warnings
  -d    Enable debug mode
```

## Environment Variables

- `ENV_FILE` - Path to environment file (default: `/opt/apps/compose/.env`)
- `PLEX_URL`, `PLEX_TOKEN` - Plex server configuration
- `JELLYFIN_URL`, `JELLYFIN_TOKEN` - Jellyfin server configuration
- `SONARR_URL`, `SONARR_API_KEY` - Sonarr configuration
- `RADARR_URL`, `RADARR_API_KEY` - Radarr configuration
- `ORGANIZR_URL`, `ORGANIZR_API_KEY` - Organizr configuration
- `TANK_MOUNT` - Tank mount point (default: `/mnt/tank`)
- `COMPOSEDIR` - Compose directory (default: `/opt/apps/compose`)

## Technical Details

- **Startup time**: ~10-50ms typical
- **Memory usage**: ~5-10MB
- **HTTP Client**: Built-in HTTP client with connection pooling and timeout handling
- **Concurrency**: Can easily be extended to make API calls concurrently
- **Error Handling**: Robust error handling with graceful degradation
- **Type Safety**: Strongly typed data structures for API responses
- **Optional Dependencies**: `figlet`, `lolcat`, `sensors`, `vnstat`, `docker` (features work without them)

## Installation

1. Build the binary
2. Copy to `/usr/local/bin/` or another location in your PATH
3. Set up environment variables or `.env` file
4. Run `motd` on login by adding to your shell profile

```bash
# Using Makefile
make install

# Or manually
sudo cp bin/motd /usr/local/bin/
sudo chmod +x /usr/local/bin/motd
```

## Cross-Compilation

Build for different platforms (outputs to `bin/` directory):

```bash
# Build all platforms
make cross-compile

# Or manually for specific platforms:
mkdir -p bin

# Linux AMD64
GOOS=linux GOARCH=amd64 go build -ldflags="-s -w" -o bin/motd-linux-amd64 main.go

# Linux ARM64
GOOS=linux GOARCH=arm64 go build -ldflags="-s -w" -o bin/motd-linux-arm64 main.go

# macOS AMD64
GOOS=darwin GOARCH=amd64 go build -ldflags="-s -w" -o bin/motd-darwin-amd64 main.go

# macOS ARM64 (Apple Silicon)
GOOS=darwin GOARCH=arm64 go build -ldflags="-s -w" -o bin/motd-darwin-arm64 main.go

# Windows AMD64
GOOS=windows GOARCH=amd64 go build -ldflags="-s -w" -o bin/motd-windows-amd64.exe main.go
```


