# Hello Zig

This example demonstrates a basic project for using the `Zigler` library to write
low-level NIFs for a Nerves device.  This project demonstrates zig code embedded
into an elixir module and how to call out to a zig code file *external* to the
embdedded elixir module.

Notably, no configuration is necessary to get proper cross-compilation between
host and target architectures.

The only thing you need to activate zigler is the dependency in your `mix.exs`:

```
{:zigler, "~> 0.3.1", runtime: false}
```

You might want to use Zig for any of the following things:

- low level code that requires interaction with OS syscalls not available
  directly through the BEAM.
- performance-sensitive code which requires numerical computation
- wrapping an existing C ABI `.so` or `.a` library.

## Hardware

The example below assumes a Raspberry Pi 3, connected over the Wifi.  Other ARM-
targets may work, but have not necessarily been tested yet.  Please post
cross-compilation bug reports to the issue tracker here:

https://github.com/ityonemo/zigler/issues

## How to Use this Repository

0. Go to the app directory

1. Set up your build environment

```shell
export MIX_TARGET=rpi3
export NERVES_NETWORK_SSID=your_wifi_name
export NERVES_NETWORK_PSK=your_wifi_password
```

2. Get dependencies, build firmware, and burn it to a MicroSD card

```shell
mix deps.get
mix firmware
mix firmware.burn
```

3. Insert the SD card into your target board and then turn on the RPi

4. Wait for the RPi to finish booting

  The RPi will show up on the network as `nerves.local`. If your computer
  does not support mDNS or if your network filters multicast, check your
  router or use `arp-scan` to find the IP address.

5. SSH into your RPi

6. Execute `HelloZig.hello()`

7. You should see it output the atom `:world`

## Learn More

- Official docs: https://hexdocs.pm/nerves/getting-started.html
- Official website: https://nerves-project.org/
- Source: https://github.com/nerves-project/nerves

- Zig language docs: https://ziglang.org/
- Zigler docs: https://hexdocs.pm/zigler
