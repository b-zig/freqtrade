Special thanks to @Tiddes on the NFI discord for the python updates. 

This Freqtrade modification is intended to help with the Kucoin candle endpoint rate limiting beyond their normal constraints. 

In order to build locally complete the following: 

git clone https://github.com/b-zig/freqtrade.git
cd freqtrade
docker build \
  --no-cache \
  --pull \
  -t freqtradeorg/freqtrade:kucoincustom .

In your docker-compose.yml be sure to update your image to: freqtradeorg/freqtrade:kucoincustom

<h2>EXAMPLE: </h2>
---
version: '3'
services:
  freqtrade:
    image: freqtradeorg/freqtrade:kucoincustom
    # image: freqtradeorg/freqtrade:develop
    # Use plotting image
    # image: freqtradeorg/freqtrade:develop_plot
    # Build step - only needed when additional dependencies are needed
    # build:
    #   context: .
    #   dockerfile: "./docker/Dockerfile.custom"
    restart: unless-stopped
    container_name: freqtrade
    volumes:
      - "./user_data:/freqtrade/user_data"
    # Expose api on port 8080 (localhost only)
    # Please read the https://www.freqtrade.io/en/stable/rest-api/ documentation
    # before enabling this.
    ports:
      - "127.0.0.1:8080:8080"
    # Default command used when running `docker compose up`
    command: >
      trade
      --logfile /freqtrade/user_data/logs/freqtrade.log
      --db-url sqlite:////freqtrade/user_data/tradesv3.sqlite
      --config /freqtrade/user_data/config.json
      --strategy SampleStrategy

