## Now with web!

Time to add [Phoenix](https://phoenixframework.org) to your firmware.

```
# Assuming you're in the fw directory, we need to move one level up

$ cd ..

$ mix archive.install https://github.com/phoenixframework/archives/raw/master/phoenix_new.ez

$ mix phoenix.new ui --no-ecto
```

We'll also need to tweak our configuration a little. In `ui/config/prod.exs`, you'll want to comment out this section:

```
config :ui, Ui.Endpoint,
  http: [port: {:system, "PORT"}],
  url: [host: "example.com", port: 80],
  cache_static_manifest: "priv/static/manifest.json"
```

  Then, in `fw/config/config.exs`, we'll add some configuration. Make sure you replace `<your_linkit_ip>` with the IP address of your Linkit

```
config :ui, Ui.Endpoint,
  http: [port: 80],
  url: [host: "<your_linkit_ip>", port: 80],
  secret_key_base: "#############################",
  root: Path.dirname(__DIR__),
  server: true,
  render_errors: [accepts: ~w(html json)],
  pubsub: [name: Ui.PubSub],
  check_origin: ["<your_linkit_ip>"]

```

Now to burn the firmware we're going to need to use the production Mix env. We'll need to prepare the assets

```
$ cd ../ui
$ mix deps.get
$ MIX_ENV=prod mix compile
$ MIX_ENV=prod mix phoenix.digest


$ cd ../fw
$ MIX_ENV=prod mix firmware
```

Once you've burned that firmware, you should be able to connect to your device through your web browser.
