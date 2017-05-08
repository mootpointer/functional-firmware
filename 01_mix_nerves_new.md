## mix nerves.new


Now that we've got Nerves and friends installed on our machines we can look at creating our first nerves project. The bootstrap archive we just installed makes that nice and easy

We're going to start by making an umbrella project. This allows us to separate our firmware from other dependencies that we're going to want to build and test on your own machine

```
# Create our umbrella project
# You can replace "blinky" with whatever you want
# to call your project.
$ mix new --umbrella blinky

$ cd blinky/apps

$ mix nerves.new fw
```

You'll be asked if you want to fetch and install dependencies. We do! Once that's done we can have a poke around in the project.

```
$ cd fw
$ ls
```

Now that we've got this done, we can move on to [preparing your Linkit](02_prepare_linkit)
