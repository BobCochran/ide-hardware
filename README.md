# IDE-hardware

Extensions to the Arduino IDE 1.5.x series to support additional hardware.

This package adds a "JeeLabs AVR Boards" entry to the Tools -> Boards menu.

The software provided in this package  will allow you to program the bootloader 
on the JeeNode Micro device and to additionally upload sketches to the Micro.
 

# REQUIRED HARDWARE:

JeeNode Micro device sold by jeelabs.net or moderndevice.com.
It is most convenient to install female headers on the MOSI/MISO/SCK/RST
pins of the Micro, but you can get by with standard pins and the wires
from modified extension cables.

At least one other Arduino device which is programmed as a dedicated ISP.
It is most convenient to do this with a JeeNode V6 device that has been 
programmed using the isp_flash.ino which you can find in the jeelib 
library maintained by Jean-Claude Wippler.

It is most convenient to use a "JeeNode Flash Board" for the purpose
of programming the JeeNode Micro. A kit can be obtained from the sources mentioned 
above. 

Small breadboards are helpful.

Extension cables with male-female wire ends and/or female-female wire ends.

FTDI cable in the appropriate voltage range or a Modern Device USB BUB device.
If you use a USB BUB, you will need an appropriate USB cable for 
connection to the Arduino device which will serve as the programmer.

A spare LED and 330 Ohm resistor is nice to have so that you can immediately
test an "LED blinking" sketch once a bootloader has been put on the JeeNode 
Micro and you can then test whether a sketch can be uploaded to it successfully.

# PHOTO ARCHIVE

See the hardware_example_photos folder for images of different development boards
used by others to program the JeeNode Micro.

# REQUIRED SOFTWARE:

Arduino IDE, version 1.5.x or higher

This software package. It primarily contains device files which are specific to
erasing, bootloader and uploading operations on the ATTINY84 chip that is used in
the JeeNode Micro.

If your intent is to use a JeeNode V6 device in order to program the JeeNode
Micro, you must first upload the isp_flash.ino sketch to this JeeNode V6, which we
will call the "programmer".

# HARDWARE SET-UP

It is assumed that you have a JeeNode Micro device onto which you have soldered
the antenna. You wish to program the ATTINY84 chip on this device using the Arduino
IDE. We will call this JeeNode Micro the "target" board.

You should also have soldered female headers to the MOSI/MISO/SCK/RST
pins of the Micro and your choice of male or female pins to the remaining pins.
It is convenient, but not needed, to solder a 20mm CR2032 battery holder to the
provided + and - pins on the underside of the micro. (Note that the battery holder
body will tend to butt tightly against the DIO2/Arduino 8 and AIO2/Arduino 7 pins of
the Micro if you are using right-angle male headers, which will bend but not break
them.) 

In the example setup, it is also assumed you have a JeeNode V6 to act as the 
Arduino "programmer". Also, we assume you have a "JeeNode Flash Board" which has
been assembled with headers, reset button, resistor and LED. It is worth repeating 
that this JeeNode V6 must have already been programmed with the isp_flash.ino 
sketch so that it is prepared to act as a programmer device.

The Flash Board must be plugged into all 4 of the "Ports" of the JeeNode V6.

Now we need to connect the 2X3 ISP pins of the flash board to the JeeNode Micro.

1. Connect Pin 1 (MISO) to the MISO pin of the JeeNode Micro.
2. Connect Pin 2 (VCC) to the +3v on the JeeNode Micro.
3. Connect pin 3 (SCK) to the SCK pin of the JeeNode Micro.
4. Connect Pin 4 (MOSI) to the MOSI pin of the JeeNode Micro.
5. Connect Pin 5 (RESET) to the RST pin of the JeeNode Micro.
6. Connect Pin 6 (Ground) to the GND pin of the JeeNode Micro.

Connect either an FTDI cable capable of the proper 3.3v logic voltage or a
Modern Device USB BUB configured for 3.3v logic voltage to the 6 pin programming header
of the JeeNode v6. If you use the USB BUB, connect an appropriate USB cable to
it and a convenient USB port on your host computer. The FTDI cable is itself a 
USB cable, plug the other end of it into a convenient USB port on the host computer.

These JeeLabs blog posts will assist you with hardware setup.

http://jeelabs.org/2013/03/21/programming-the-jn%C2%B5-at-last/

http://jeelabs.org/2013/03/20/programming-the-jnu-again/

http://jeelabs.org/2013/03/03/programming-the-jnu-v3-part-1/

There are other devices that can be used as the programmer, and some may offer
less "bother" and complexity than the procedure shown above. To get some idea of
what other JeeNode Micro users are using as programmer devices, see the 
hardware_example_photos folder in this distribution.
 
# Installation and use of this software package

The software is meant to work with the Arduino IDE, version 1.5.x or higher. It
has been tested successfully on versions 1.5.2, 1.5.4, and 1.5.4r2. When installed
on the host system, a preferences.txt file will be created. This file contains a
"sketchbook path" option that tells the path to the user's sketchbook folder. You
may want to note down this path before beginning software installation.

* Make sure your IDE's "Sketchbook location" contains a `hardware` folder. Create
  a "hardware" folder if you do not have one in the sketchbook.  
* From a command prompt or terminal window, change directory to this 
  {sketchook path}/hardware directory. 
* Download or "git clone" this project at <https://github.com/jcw/ide-hardware>
* Rename the download to `jeelabs` (!) and put it inside the `hardware` folder.
  You should have a new folder named {sketchook path}/hardware/jeelabs.
* Edit the {sketchook path}/hardware/jeelabs/avr/boards.txt folder as needed. 
  Note particularly that the setting jnmicro.bootloader.file is pointing at an
  8 MHz bootloader for the ATTiny84; but there are two other bootloader hex files
  in the same directory that you may prefer using.
* Similarly, check that the platform.txt file is to your preference.
* Restart the Arduino IDE if it was still running, so it'll pick up the changes.
  That is, quit the Arduino IDE and launch it again.
* Connect USB cable to the JeeNode V6 device that is being used as the programmer. 
  This JeeNode V6 should be connected to a JeeNode Micro device as described in
  "Hardware Set-Up", above.
* Upon restarting the Arduino IDE, you should see a new "JeeLabs AVR boards" 
  entry in the Tools -> Board menu.
* Select "JeeNode Micro" from the above menu.
* Select Tools -> Programmer -> Arduino as ISP.
* To set the fuses and optional boot loader, use Tools -> Burn Bootloader.
  Burning a bootloader generally requires that the ATTINY84 chip first be erased, 
  and then the fuses set and the new bootloader installed. There will be quite a 
  lot of output in the serial console window of the Arduino IDE. You may want to scroll
  this window to check for error messages.
* To upload a sketch, you can then use the standard "Upload" button. Again, there
  will be quite a lot of output to the serial console window. A nice way to test that
  your JeeNode Micro is working is to upload a sketch that causes an LED connected
  to one of the Micro's digital pins to blink.  
* Apparently, uploading a sketch will wipe out the bootloader on an ATTINY84 device. 
  This is per advice from other contributors. Additional detail on this will be
  added as it is learned.


# License

Material and code added by the BobCochran/ide-hardware fork (that is, this fork)
is Creative Commons licensed. 

Material from the jcw/ide-hardware is licensed as GNU Lesser GPL, same as the 
original code (see below).

# Credits

This fork of the jcw/ide-jardware repository was created by Bob Cochran with
considerable support and assistance from "JohnO", "Martynj" and "Wolfpackmars2" 
on the JeeLabs.net Support forums. This fork was made possible through a posting 
by "Henry" on the forums. Please see this thread:

http://jeelabs.net/boards/7/topics/2986?page=1&r=3126

Support and advice from "JohnO" were key to enabling BobCochran and Henry 
to actually bootload and then upload and execute sketches to the JeeNode Micro.

Major changes in this fork are to correct and complete the boards.txt and
platform.txt files, and to provide additional documentation in this README.txt
file.

# Notes from the original jcw/ide-hardware project:


This code was adapted from <http://code.google.com/p/arduino-tiny/>:

> Arduino-Tiny is an open source set of ATtiny "cores" for the Arduino platform.
> 
> The Arduino platform currently supports Atmel ATmega processors. There is a need for the Arduino platform to work with physically smaller DIP package processors. The intent of this project is fulfill that need. Specifically, our goal is to provide a core that enables Arduino users to work with the ATtiny84 (84/44/24), ATtiny85 (85/45/25), and ATtiny2313 processors.

More information is available in `avr/readme.txt`:

> Arduino-Tiny is based on work by David A. Mellis, René Bohne, R. Wiersma, 
Alessandro Saporetti, and Brian Cook.

The main change was to move things around to insert an extra `avr` folder and
to include the necessary boards.txt + platform.txt + programmers.txt files.
