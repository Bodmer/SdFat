# SdFat
A version of SdFat that works with the JPEGDecoder library.

This version has one small modification to make the created SD class members 'global' so
they can be used in a sketch and by the JPEGDecoder library.
(The SD library makes the equivalent class global without modifications)
There may be an easier way to do this but it works OK.

The line added is 'extern SdFat SD;' at around line 283. Thus the following line sequence appears in the
SdFat.h file:

  extern SdFat SD; //<<= Line to add, the next 2 lines are ALREADY in the file, they
                   //    are included here just to help locate the right place!
  //==============================================================================
  #if SD_SPI_CONFIGURATION >= 3 || defined(DOXYGEN)


The hardware SPI pins allocated on the Mega are 50, 51 and 52. On the Due these
are not connected to the hardware SPI function, so to use the Due with TFT shields that
use the Mega allocated SPI pins it is necessary to bitbash the Due pins.  To do this the
following changes have been made to the SdFatConfig.h file as indicated by =>> below:

=>>    #define SD_SPI_CONFIGURATION 2  // Set to 0 for Mega, 2 for Due
  //------------------------------------------------------------------------------
  /**
     If SD_SPI_CONFIGURATION is defined to be two, these definitions
     will define the pins used for software SPI.

     The default definition allows Uno shields to be used on other boards.
  */
  /** Software SPI Master Out Slave In pin */
=>>             uint8_t const SOFT_SPI_MOSI_PIN = 51;
  /** Software SPI Master In Slave Out pin */
=>>             uint8_t const SOFT_SPI_MISO_PIN = 50;
  /** Software SPI Clock pin */
=>>             uint8_t const SOFT_SPI_SCK_PIN  = 52;
  //------------------------------------------------------------------------------
