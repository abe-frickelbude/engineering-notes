

# Integration of MySmartUSB Light programmer with PlatformIO

## Programmer setup

* The programmer has to be flashed with the `AVR911` firmware, the `STK500` no longer works   correctly for some reason
* Use AVRDude on CLI to check that the programmer is operational:
```
avrdude.exe -P COM3 -p m328p -c avr911 -D -U flash:r:test.hex:r
``` 

## PlatformIO integration

Add the following into a project's `platformio.ini` file:

```
[env:atmega328]
platform = atmelavr
board = atmega328p
framework = arduino
upload_protocol = avr911
upload_speed = 19200
```

* The `upload_speed` setting is crucial, as auto-negotiation apparently doesn't always
work and will prevent access to the programmer
* The `board` must be set precisely, i.e. an `Atmega328P` must literally be referred as such, and not just as `atmega328` as this gives the wrong device signature to AVRDude, which then refuses
to talk to the MCU, complaining about the said incorrect signature.
