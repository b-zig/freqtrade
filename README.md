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



