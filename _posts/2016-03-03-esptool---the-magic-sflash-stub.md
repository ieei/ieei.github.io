---
layout: post
title: ESPtool - the magic sflash stub
author: Haakon Sporsheim
date:  2016-03-03 12:00:00
categories: dev
image: /img/r2_esptool_sflash_stub.png
tags: esp8266 radare
---
The open source ESP8266 [esptool][themadinventor-esptool] that's part of the
[esp-open-sdk][esp-open-sdk] is used as a tool to create a firmware image
from elf image/binary.
It is also used to flash/program an ESP8266 with this firmware image.
In addition you can do the opposite, download a firmware image.

### SFLASH_STUB
Browsing through the `esptool.py` source code I found an interesting piece of
binary blob I just had to take a closer look at.
{% highlight python %}
# Sflash stub: an assembly routine to read from spi flash and send to host
SFLASH_STUB = "\x80\x3c\x00\x40\x1c\x4b\x00\x40\x21\x11\x00\x40\x00\x80\xfe" \
              "\x3f\xc1\xfb\xff\xd1\xf8\xff\x2d\x0d\x31\xfd\xff\x41\xf7\xff" \
              "\x4a\xdd\x51\xf9\xff\xc0\x05\x00\x21\xf9\xff\x31\xf3\xff\x41" \
              "\xf5\xff\xc0\x04\x00\x0b\xcc\x56\xec\xfd\x06\xff\xff\x00\x00"
{% endhighlight %}

It is used in the following python function.
{% highlight python %}
""" Read SPI flash """
def flash_read(self, offset, size, count=1):
    # Create a custom stub
    stub = struct.pack('<III', offset, size, count) + self.SFLASH_STUB

    # Trick ROM to initialize SFlash
    self.flash_begin(0, 0)

    # Download stub
    self.mem_begin(len(stub), 1, len(stub), 0x40100000)
    self.mem_block(stub, 0)
    self.mem_finish(0x4010001c)
{% endhighlight %}

This means the stub is prefixed with 3x 32bit integers, respectively
`offset`, `size` and `count`.
The stub plus prefix is flashed into memory @ `0x40100000` and then execution
starts @ `0x4010001c` meaning that first 4x 32bit integers of the stub
is probably data.

### Radare
I figured, this was a perfect use case of showing how to use [radare][rada.re].
Here it is:
[![asciinema]({{ page.image }})][r2_asciinema]


There you have it!
esptool uploads the sflash stub and executes it.
The stub itself contains a small function which calls two functions in a loop.
First `SPIRead` is called to fetch a block from flash into RAM.
Then `send_pakcet` is called to send this block back over UART.
Both `SPIRead` and `send_packet` resides in ROM and are so called
ROM functionality.

[themadinventor-esptool]: https://github.com/themadinventor/esptool
[esp-open-sdk]: https://github.com/pfalcon/esp-open-sdk
[rada.re]: //rada.re
[r2_asciinema]: https://asciinema.org/a/a1c9znc34jl8ztm4ien7n2ldm
