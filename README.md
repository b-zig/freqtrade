Special thanks to @Tiddes on the NFI discord for the python updates. 

This Freqtrade modification is intended to help with the Kucoin candle endpoint rate limiting beyond their normal constraints. 

In order to build locally complete the following: 

git clone https://github.com/b-zig/freqtrade.git<br>
cd freqtrade<br>
docker build --no-cache --pull -t freqtradeorg/freqtrade:kucoincustom .

In your docker-compose.yml be sure to update your image to: freqtradeorg/freqtrade:kucoincustom

<i> PLEASE NOTE: Pandas-TA is included in this image... YOU DO NOT need to do a custom build dockerfile to install it</i>

<h2>EXAMPLE:</h2>
<br>
---<br>
version: '3'<br>
services:<br>
  freqtrade:<br>
    image: freqtradeorg/freqtrade:kucoincustom<br>
    # image: freqtradeorg/freqtrade:develop<br>
    # Use plotting image<br>
    # image: freqtradeorg/freqtrade:develop_plot<br>
    # Build step - only needed when additional dependencies are needed<br>
    # build:<br>
    #   context: .<br>
    #   dockerfile: "./docker/Dockerfile.custom"<br>
    restart: unless-stopped<br>
    container_name: freqtrade<br>
    volumes:<br>
      - "./user_data:/freqtrade/user_data"<br>
    # Expose api on port 8080 (localhost only)<br>
    # Please read the https://www.freqtrade.io/en/stable/rest-api/ documentation<br>
    # before enabling this.<br>
    ports:<br>
      - "127.0.0.1:8080:8080"<br>
    # Default command used when running `docker compose up`<br>
    command: ><br>
      trade<br>
      --logfile /freqtrade/user_data/logs/freqtrade.log<br>
      --db-url sqlite:////freqtrade/user_data/tradesv3.sqlite<br>
      --config /freqtrade/user_data/config.json<br>
      --strategy SampleStrategy<br>
