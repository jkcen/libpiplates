# C library for the PI-Plates I/O boards
## made for Raspberry PI (libpiplates)

## API overview

Help would be nice - ThX.

## API Defines and Functions

Help would be nice - ThX.

####PI-Plates GPIO pin and board base address structure####
```
struct config {
	// Digitial input pin - Signal to interrupt (BCM pin 22)
	uint8_t pinInterrupt

	// Digital output pin - Signal to control SPI bus transfer (BCM pin 25)
	uint8_t pinFrameControl

	// PI-Plates specific SPI board base address
	uint8_t boardBaseAddr

	// SPI BUS channel number (0=/dev/spidev0.0 or 1=/dev/spidev0.1) Default is 1
	uint8_t spiChannel
};
```

####PI-plates board handle structure####
```
struct board
{
	// GPIO/SPI configuration
    config_t config;

    // The PI-Plates board address in range 0 to 7
    uint8_t address;

    // The PI-Plates board type 1=RELAYplate 2=DAQCplate 3=MOTORplate
    uint8_t type;

    // In case of the DAQCplate the Vcc value in volts
    float vcc;
};
```

####API Version structure####
```
struct version
{
	const long major;
	const long minor;
	const long build;
	const long revision;
};
```

####Initialize GPIO/SPI configuration structure####
To communicate with the PI-Plates boards you have to initialize the GPIO/SPI communication configuration.
**Note** that the pin numbers follows wiringPi GPIO layout and will be translated to the Broadcom pin layout.
The C API library initializes the wiringPi with BCM pin layout. Function parameters:
- **spiChannel** Use constant PP_SPI_IO_CHANNEL for default
- **wpiPinINT** Interrupt signal pin (wiringPi=3 BCM=22)
- **wpiPinFrame** SPI frame signal pin (wiringPi=6 BCM=25)
- **boardBaseAddr** The PI-Plates board address
- **pConfig** Pointer to the configuration structure
- **return** 0 if succsess otherwise signal an error

```
int initConfig(
			const uint8_t spiChannel,
			const uint8_t wpiPinINT,
			const uint8_t wpiPinFrame,
			const uint8_t boardBaseAddr,
			config_t* pConfig);
```

####Initialize the PI-Plate boards by specified board type####
Function to initialize the all PI-Plates boards by specified board type. Each available board becomes a board_t
handle allocated in a global board list. You must call **initConfig()** first to get the configuration for the
board GPIO/SPI communication parameters. Function parameters:
- **type** One of the predefied board types (RELAY=1, DAQC=2 or MOTOR=3)
- **return** 0 if succsess otherwise signal an error
```
int initBoards(uint8_t type, const config_t* pConfig);
```

## Requirements and Dependencies

Help would be nice - ThX.

### Thrid party dependencies

	- wiringPi library for Raspberry PI

### Copyright (c) 2016-2017 by B. Eschrich, (E)mpire (O)f (F)un Guild
### All rights reserved.


# Changes -
