## Preparing your Linkit Smart 7688

There are a couple of steps to getting your Linkit ready to go. We'll start by placing it on the breadboard, and then connecting to it with a serial cable. Once we're done with that, we'll flash a new bootloader and kernel for good measure.

### Putting your Linkit on the breadboard

Your breadboard is just big enough to fit your linkit and a couple of extra components. You'll find it best to have your linkit at the top of the breadboard, with one row of holes accessible either side.

The pin-pitch and hole-pitch can be slightly misaligned sometimes, but the careful application of some firm pressure should get your linkit seated in the breadboard.

### Connecting with a serial cable

We're going to use the USB FTDI adapter provided to connect to the Linkit. We'll use some jumper leads for the job.

| FTDI Pin | Linkit Pin |
| -------- | ---------- |
| RX       | 9          |
| TX       | 8          |
| GND      | GND        |
| VCC      | VCC        |



### Connecting the console

If you're on Linux, there's an extra step required to get permissions to use the
serial port. It's owned by the `dialout` group so you'll need to make sure your
user is in that group.

```
# Check which groups you're already in
$ groups

# Add yourself to the dialout group
$ sudo gpasswd --add ${USER} dialout
```

You may need to log out and in again for this to take effect.

Now we're going to talk to our Linkit over the UART interface that we've connected the USB-Serial adapter to. First we need to find the adapter device.

On macOS:

```
$ ls /dev/cu.*

Should list a few devices, but we're looking for a USB serial device.

```

On Linux:
```
$ ls /dev/ttyUSB*

```
In theory there should only be one device, but I don't have access to linux to check.

Now with the device we've found, we connect to it using picocom.

```
$ picocom -b 57600 /path/to/your/serialport
```

Now, press the `MPU` button on the Linkit and you should see some text scrolling up the screen!

### Flashing the bootloader and kernel

To flash the bootloader, plug  USB drive with the bootloader and kernel image on it into the Linkit using the USB host cable.

Then, press the `MPU` button on the Linkit and hold down the `b` key in your serial console until you see it searching for and loading the new bootloader. The device will automatically reboot once it's done.

To flash the kernel, with the USB drive still plugged in, press the `MPU` to restart the Linkit and hold the `5` key in your serial console until you see the new kernel installing. The device will automatically reboot once it's done.

With this done, we've almost got nerves loaded! Next step is to [burn our firmware](burn_firmware)
