# SdFat
A version of SdFat that works with the JPEGDecoder library.

This version has one small modification to make the created SdFat class 'global' and allow it to be reffered to as SD. This change means member functions can be used both in a sketch and by the JPEGDecoder library.
(The standard Arduino IDE "SD" library makes the equivalent SD class global without modifications)
There may be an easier way to do this but it works OK.

The line added is:

```
extern SdFat SD;
```
at around line 283 in the SdFat.h file.

The hardware SPI pins allocated on the Mega are 50, 51 and 52. On the Due these
are not connected to the hardware SPI function, so to use the Due with TFT shields that
use the Mega allocated SPI pins it is necessary to bitbash the Due pins.  To do this the
changes have been made to the SdFatConfig.h file:



```
#define SD_SPI_CONFIGURATION 2

uint8_t const SOFT_SPI_MOSI_PIN = 51;

uint8_t const SOFT_SPI_MISO_PIN = 50;

uint8_t const SOFT_SPI_SCK_PIN  = 52;
```
