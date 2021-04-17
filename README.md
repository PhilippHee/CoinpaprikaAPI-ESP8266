# CoinpaprikaAPI-ESP8266

**Use the ESP8266 to get information from the Coinpaprika API**

With this project/sketch, the API of Coinpaprika (`https://api.coinpaprika.com`) can be used and current information of the different coins/cryptocurrencies (e.g. Bitcoin, Ethereum) can be retrieved.

This project is based on the sample project/sketch "HTTPSRequest" by Ivan Grokhotkov from the ESP8266WiFi library and on the repository/library "arduino-coinmarketcap-api" by Brian Lough ([GIT](https://github.com/witnessmenow/arduino-coinmarketcap-api)).

[![license](https://img.shields.io/badge/license-MIT-orange.svg)](LICENSE)

## Preparations
Before the project/source code can be used, a few preparations have to be made. This includes the configuration of the Arduino IDE and the installation of required libraries.

### Boardmanager
The Arduino IDE is not configured for the ESP8266 by default, so you have to install an additional boards manager first (see also [here](https://github.com/esp8266/Arduino)). For this you have to add the following boards manager URL in the Arduino IDE under *File > Preferences* in the *Settings* tab: `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

Then the appropriate board can be installed via *Tools > Board > Boards Manager...* by searching for *esp8266* ([**esp8266** by ESP8266 Community](https://github.com/esp8266/Arduino)) in the search bar. After that, the appropriate board must be selected from the drop-down list (*Tools > Board*). In this project a D1 Mini ESP8266 ([Amazon Link](https://amzn.to/2QwETcy)) is used, the correct entry for this is *LOLIN(WEMOS) D1 R2 & mini*. Installing the board also installs many libraries that are specific to this board, such as for using the WiFi module.

To be able to use the board after connecting it to the computer, the correct COM port must also be selected in the IDE under *Tools > Port*. A manual installation of the driver of the USB interface was not necessary, but it may be.

### Board settings
This project/sketch uses the following settings in the Arduino IDE (*Tools*):
|Setting|Value|
|-|-|
|Board|LOLIN(WEMOS) D1 R2 & mini|
|Upload Speed|921600|
|CPU Frequency|160 MHz|
|Flash Size|4MB (FS:2MB OTA:~1019KB)|
|Debug port|Disabled|
|Debug Level|None|
|lwIP Variant|v1.4 Higher Bandwidth|
|VTables|Flash|
|Exceptions|Legacy (new can return nullprt)|
|Erase Flash|Only Sketch *(or: All Flash Contents)*|
|SSL Support|All SSL ciphers (most compatible)|

### Additional libraries
Additionally the following libraries are needed, which can be ...
1. searched and installed directly from the Arduino IDE (*Tools > Manage Libraries...*) or
2. downloaded from the respective GIT page and added manually to the local Arduino library directory.

|Library|Repository|
|-|-|
|**ArduinoJson** by Benoit Blanchon|[GIT](https://github.com/bblanchon/ArduinoJson)|
|**NTPClient** by Fabrice Weinberg|[GIT](https://github.com/arduino-libraries/NTPClient)|

Note: Please note the general information as well as troubleshooting tips when using the libraries!


## Source code
The source code ([**CoinpaprikaAPI-ESP8266.ino**](CoinpaprikaAPI-ESP8266.ino)) is roughly divided into the following areas/functionalities:
- establishing the WiFi connection with the home router
- querying the Coinpaprika API depending on the selected coins
- output of the coin information via the serial monitor

The information of the coin is retrieved in the function `getTickerInfo()`, e.g.:
```
CPTickerResponse ticker = getTickerInfo("btc-bitcoin");
```

The information (return value) is collected in a structure that has the following values:
```
struct CPTickerResponse {
  String id;
  String name;
  String symbol;
  unsigned int rank;
  double price_usd;
  double price_btc;
  double volume_24h_usd;
  double market_cap_usd;
  double circulating_supply;
  double total_supply;
  double max_supply;
  double percent_change_1h;
  double percent_change_24h;
  double percent_change_7d;
  unsigned long last_updated;
  String last_updated_string;
  String error;
};
```

The function `printTicker()` can be used to display the values via the serial monitor of the Arduino IDE. In the upper part of the source code you have to store your WiFi connection data and enter the coins that should be retrieved.

For more information, see the comments in the code.


## Further project
The following project continues this project, so that you can print the different coins on an external display:
**CoinpaprikaAPI-ESP8266-Display** by PhilippHee ([GIT](https://github.com/PhilippHee/CoinpaprikaAPI-ESP8266-Display))
