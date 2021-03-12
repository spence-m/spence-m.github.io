---
layout: post
title:  "Raspberry Pi Pico Hello World on Windows"
date:   2021-03-12
categories:
 - raspberry pi pico
comments: false
---

The documentation for the Raspberry Pi Pico assumes your Pico is plugged into another Raspberry Pi.

Here's how to run the Hello World sample on Windows.

The first four steps are the same so this is ripped from the original C [documentation](https://www.raspberrypi.org/documentation/rp2040/getting-started/#getting-started-with-c):

> 1. Download the 'Hello World' UF2.
> 2. Push and hold the BOOTSEL button and plug your Pico into the USB port of your > Raspberry Pi or other computer.
> 3. It will mount as a Mass Storage Device called RPI-RP2.
> 4. Drag and drop the 'Hello World' UF2 binary onto the RPI-RP2 volume. Pico will reboot

So now you've done that, the first thing we need to find out is which communication port the Pico is using.

5. Open the command prompt and run:

```
mode
```

You will see output similar to this:

```
...

Status for device COM3:
-----------------------
    Baud:            115200
    Parity:          None
    Data Bits:       8
    Stop Bits:       1
    Timeout:         OFF
    XON/XOFF:        OFF
    CTS handshaking: OFF
    DSR handshaking: OFF
    DSR sensitivity: OFF
    DTR circuit:     OFF
    RTS circuit:     ON


Status for device CON:
----------------------
    Lines:          9001
    Columns:        120
    Keyboard rate:  31
    Keyboard delay: 1
    Code page:      850
```

We can see that the Pico is `COM3` because the baud rate is set to `115200`.

6. Now, open `PuTTY`

7. Set the `Connection Type` to `Serial`

8. Set the `Serial Line` to the communication port from the previous step, which is `COM3` for me

9. Change the `Speed` to `115200`

10. Click `Open`

If you see `"Hello World"` being printed to the console then it worked :)
