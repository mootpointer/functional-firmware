## Let's play with LEDs!

### Add the ElixirALE dependency

First up we'll add the dependency to the `mix.exs`:

Look for this line:

```elixir
def deps(target) do
```

And add this to the list:

```
{:elixir_ale, "~> 0.6.2"}
```

Run `mix deps.get` again, then build and and burn your firmware, putting your card into the Linkit and restarting it.

### Power your Breadboard

1. Connect the `GND` pin from your USB-serial to the negative rail on your breadboard.
2. Add connect a jumper cable (black by convention) from the negative (`-`) rails on your breadboard to the `GND` pin on your Linkit

### Breadboard your LED

1. Put your LED on your breadboard, oriented vertically with the shorter pin toward the bottom of the board
2. Connect a jumper cable from the bottom pin of the LED to the negative rails of your breadboard
3. Connect a jumper cable from the top pin of your LED to `P12` on your Linkit

### Let's flash an LED from the console!

On your serial console, you should be at the IEx prompt.

We're going to start by bringing in the GPIO module from the ElixirALE package we just added to our firmware.

```
iex(1)> import ElixirAle.GPIO
```

Now we're going to start a process to interact with that pin we connected to the LED

```
iex(2)> {:ok, pid} = GPIO.start_link(0, :output)
```

And now we can toggle our LED using the `GPIO.write` function:

```
iex(3)> GPIO.write(pid, 1)
# Your LED should now be on, if it wasn't already.
iex(4)> GPIO.write(pid, 0)
# Your LED should now be off!
```

Okay, an LED that requires typing is not super-useful, but we're on our way!

Next up we're going to [play with buttons!](buttons)
