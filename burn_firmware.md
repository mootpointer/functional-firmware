## Burning your firmware

Once you've got your Linkit set up with the new kernel and booloader, you'll see that it's looking for the root partition.

We provide this root partition on a microSD card, and we use Nerves to put your code on it.

Once you've set up your project, you'll want to set the `MIX_TARGET` environment variable to `linkit` to save some typing.

```
$ export MIX_TARGET=linkit
```

Now we need to get the required packages for this architecture:

```
$ mix deps.get
```

And now we can build the firmware:

```
$ mix firmware
```

Put your microSD card in your computer, either using the USB adapter or the SD card adapter, then:

```
$ mix firmware.burn
```
You'll be asked to choose the location of the memory card. Use the size of your card as a guide for which one to select.

Sometimes the password prompt can fail to show, and the process will fail. Don't worry. Just run the command again.

## Boot into nerves

Once you've burned your firmware to the card, you can put the card into the microSD card slot on the Linkit. It's located underneath the USB ports.

Now, restart the Linkit and watch it boot up. You should end up with an IEx prompt that looks something like this:

```
Erlang/OTP 19 [erts-8.0.1] [source] [64-bit] [smp:8:8] [async-threads:10] [hipe] [kernel-poll:false] [dtrace]

Interactive Elixir (1.4.1) - press Ctrl+C to exit (type h() ENTER for help)
iex(1)>
```

You're now inside an Elixir REPL on your device, congratulations!
