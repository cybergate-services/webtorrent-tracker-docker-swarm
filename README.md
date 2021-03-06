# Docker-Bittorrent-Tracker

Docker Image for [webtorrent/bittorrent-tracker](https://github.com/webtorrent/bittorrent-tracker)

## Supported architectures

- x86-64
- arm64
- armhf

## Usage

`docker run --rm -i -t quoorex/bittorrent-tracker:latest`  
Or run this to expose the port 8100:  
`docker run --rm -p 8100:8000 -i -t quoorex/bittorrent-tracker:latest`  

## Configuration

Just pass all configurations as environment variables into the container.  

Possible values (as listed in [`config.js`](/config.js)):  

- HTTP (Enable HTTP server.): true/false
- UDP (Enable UDP server.): true/false
- WEBSOCKET (Enable websocket server.): true/false
- TORRENT_WHITELIST (List of allowed info hashes. If this option is omitted, all torrents are allowed.): hash1,hash2
- STATS (Provide tracker statistics via web interface at /stats.): true/false
- TRUST_PROXY (Trust x-forwarded-for header from reverse proxy): true/false

By default all boolean values are true and the torrent whitelist is disabled.

### Example

Running the bittorrent tracker with stats disabled:  
`docker run --rm -i -e STATS="false" -t quoorex/bittorrent-tracker:latest`  

## docker-compose

```
services:
  bittorrent-tracker:
    image: quoorex/bittorrent-tracker
    container_name: bittorrent-tracker
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - STATS=true # optionally add your configuration here
    restart: unless-stopped
```
