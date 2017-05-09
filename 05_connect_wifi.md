## Let's Add WiFi

You can run a web server on your embedded device!

We'll need to set up wifi first.

Add this deps to your target deps list:

```
{:nerves_interim_wifi, "~> 0.2.0"}

```

And add some functions to your project's `application.ex`

Before the last `end` add:

```
  def init_kernel_modules() do
    System.cmd "modprobe", Application.get_env(:fw, :wifi_modules)
  end

  def init_wifi_network() do
    Nerves.InterimWiFi.setup @interface, Application.get_env(:fw, @interface)
  end
```

And add two workers to the list of children:

```
worker(Task, [fn -> init_kernel_modules() end], restart: :transient, id: Nerves.Init.WifiKernel),
worker(Task, [fn -> init_wifi_network() end], restart: :transient, id: Nerves.Init.WifiNetwork),

```

Just after the module definition add:

```
@interface :wlan0
```

Finally, open up `config/config.exs` and add the wireless configuration.

You'll need to set the ssid and PSK to your own network.

```
config :fw, :wlan0,
  ssid: "Blinkenlichten", 
  key_mgmt: :"WPA-PSK",
  psk: "Stand Back"
  
config :fw, :wifi_modules, ["mt7603e"]

```

Now burn that firmware, and you should be able to see your device connecting to the wifi and receiving a DHCP lease in the serial console.

Since you've got wifi, it's probably time to [add a web server](06_add_phoenix)
