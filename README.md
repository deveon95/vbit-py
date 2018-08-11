# vbit-py
This project is used to generate teletext suitable for decoding in a TV. This project is the hardware driver part and it relies on being given a teletext stream. Teletext streams can be generated by vbit2. This project relies on the vbit inserter hardware and a raspberry pi.
## teletext stream to vbit hardware, in python

This works the same as raspi-teletext but drives the vbit hardware rather than a Raspberry Pi.

It runs on the latest version of Raspberry Pi.

## Initial tests
### i2c bus and video chips
Check that the i2c bus and chips are responding correctly
```bash
pi@raspberrypi:~ $ i2cdetect 1
WARNING! This program can confuse your I2C bus, cause data loss and worse!
I will probe file /dev/i2c-1.
I will probe address range 0x03-0x77.
Continue? [Y/n] y
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- 25 -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- 44 -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: -- -- -- -- -- -- -- --
```
You should get a response from 25 and 44 if the vbit chips are working. If not you should look in the Raspbarry Pi config that i2c is enabled.
### video path
This test configures the video chips. Put PAL video in vbit on the left hand connector. Run PAL video from the right hand output to a TV monitor. Run the shell script vbit-i2c.sh. The picture should be passed through the video chain and appear on the monitor.
### spiram
This test checks that the spiram is working. This test does not need video running. The resulting array should be the same as the one that was written to the spiram. If errors or randomness happens try reducing the spi bus speed as mentioned in the source code.
```bash
pi@raspberrypi:~/vbit-py $ python spi.py
[65, 66, 67, 68, 77, 77, 77, 77, 77, 77, 77, 55, 77, 77, 77]
clean up
```
