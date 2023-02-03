
# ATTiny13(A) programming notes

## Setting fuses on PlatformIO

* The fuses are automatically calculated from `board_hardware.*` flags ONLY 
   when using one of the `*Core` frameworks, as outlined in <https://docs.platformio.org/en/stable/platforms/atmelavr.html#fuses-programming>
* Otherwise (i.e. when doing "bare-metal" programming without MicroCore) the
  `board_fuses.lfuse` and `board_fuses.hfuse` must be calculated manually and specified in the `platformio.ini` file!

### AvrDude troubles

* Current configuration with MyAvrISP programmer fails to set fuses if using AvrDude, and requires the original windows 
  software `myAVR_progtool.exe` to set the fuse bits properly!

## Clock settings

* The factory-preset fuse configuration for ATTiny13 ships with the `CKDIV8 (bit 4)` fuse bit in the lower fuse enabled.
  Combined with the default internal RC oscillator frequency of `9.6 Mhz` this gives an effective clock frequency of `1.2 Mhz`!!
  This is not clearly mentioned in any DIY guides, tutorials, HOWTOs, official PlatformIO docs etc! In order to have the
  correct clock this fuse bit must be set to `1`.
* Many existing examples on the interwebs appear to have been made for the above default configuration, so those 
  may break in unpredictable ways when running at full 9.6 Mhz. For example, a few examples of driving I2C displays
  (OLED, MAX7219 etc) do not work properly because the communication routines no longer use appropriate timings / delays.
  * The clock can be dynamically influenced by using `clock_prescale_set(clock_div_2)` (imported from `<avr/power.h>`)
    to change the clock prescaler settings. If called once at the very beginning of the `main`, this achieves the same 
    effect as setting the CKDIV fuse bit, but is more flexible as it can divide the clock by different factors. 


## MicroCore