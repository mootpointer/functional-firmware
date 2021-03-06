# Let's get started!

## Requirements:
There's a few things we need to work with the hardware we've got, here's a list so if you want to get them early, you can!

   
### macOS

```
$ brew update
$ brew install erlang
$ brew install elixir
$ brew install fwup squashfs coreutils
```

Also, you'll need to install [the driver for the USB-Serial adapter](http://www.ftdichip.com/Drivers/VCP/MacOSX/FTDIUSBSerialDriver_v2_3.dmg)

   
### Linux

```
# Install Erlang Solutions repo
$ wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && sudo dpkg -i erlang-solutions_1.0_all.deb

$ sudo apt-get update

# Install Erlang
$ sudo apt-get install esl-erlang

# Install Elixir
$sudo apt-get install elixir

# Install askpass for burning firmware
$ sudo apt-get install ssh-askpass

# Install squashfs for constructing firmware images
$ sudo apt-get install squashfs-tools

# Install picocom for talking to the device over the serial adaptor
$ sudo apt-get install picocom
```

### Windows

Some people have had success using the Windows Subsystem for Linux or a virtual machine... So I guess follow the Linux instructions?


## Install Nerves

First up, make sure our tools are up to date, so we'll do these:

```
$ mix local.hex
$ mix local.rebar
```

Then we'll install the Nerves Bootstrap archive. This sets up mix and installs a project generator which we'll need in a moment.

```
$ mix archive.install https://github.com/nerves-project/archives/raw/master/nerves_bootstrap.ez
```

Ready? [let's create our nerves project](01_mix_nerves_new)
