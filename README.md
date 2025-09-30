<div align="center">

[![Discord](https://img.shields.io/discord/1255867192503832688?label=MakerPnP%20discord&color=%2332c955)](https://discord.gg/ffwj5rKZuf)
[![YouTube Channel Subscribers](https://img.shields.io/youtube/channel/subscribers/UClzmlBRrChCJCXkY2h9GhBQ?style=flat&color=%2332c955)](https://www.youtube.com/channel/UClzmlBRrChCJCXkY2h9GhBQ?sub_confirmation=1)
[![MakerPnP GitHub Organization's stars](https://img.shields.io/github/stars/makerpnp?style=flat&color=%2332c955)](https://github.com/MakerPnP)
[![Donate via Ko-Fi](https://img.shields.io/badge/Ko--Fi-Donate-green?style=flat&color=%2332c955&logo=ko-fi)](https://ko-fi.com/dominicclifton)
[![Subscribe on Patreon](https://img.shields.io/badge/Patreon-Subscribe-green?style=flat&color=%2332c955&logo=patreon)](https://www.patreon.com/MakerPnP)


![MakerPnP](assets/logos/makerpnp_icon_1_384x384.png)

</div>

# Linux Realtime (LinuxRT) Experimentation

This repo is for experimentation with Linux RT (aka Linux with a PREEMPT_RT kernel).

The repo contains a few small and focussed crates, all the crates with 'rt' in the name are suitable for `no_std` real-time threads.

* rt_circular_buffer - a simple circular buffer impl, suitable for RT threads. (no_std)
* rt_spsc - a single producer single consumer message queue. (no_std)
* rt_thread - for spawning real-time threads. (no_std).
* rt_time - some time related functions for scheduling. (no_std).
* server - the main app (std)
* server_rt_core - the core (no_std)
* server_rt_shared - shared code (e.g. definitions of rt<->main messages)

Any code in an `rt` crate should be lock-free, atomic-free, no-alloc, no-std with good deterministic worst-case latency (i.e. time-constant). only compiler_fences are used - AtomicBool/Int/etc, are NOT used to avoid delays from CPU core/memory synchronization on multi-core systems.

## Supported platform

Should be fine on any Linux system with a recent PREEMPT_RT kernel. e.g. a Raspberry Pi 4 with the ROS image: https://github.com/ros-realtime/ros-realtime-rpi4-image.

## Building

```
cd server
cargo build --release
```

## Running

```
sudo ./target/release/server
```

## Expected output

When it runs, it should show something like this:

```
RT thread launched
Waiting for RT system to stabilize...
.
RT thread starting with priority 80
Received message: Request(Request { index: 0, payload: StabilityChanged(Stable) })
RT recent latency values (ns): [143463, 141388, 142368, 143589, 141995, 142938, 177640, 143454, 127879, 163378, 163987, 161338, 163466, 160817, 163260, 162259, 201442, 165608, 113201, 145773, 142105, 141937, 142843, 141379, 142693, 141099, 142598, 144948, 138743, 140520, 142741, 141369, 141812, 143144, 141328, 142216, 141826, 179954, 143620, 222543, 166413, 162282, 163707, 163206, 162297, 162537, 162239, 200904, 160866, 110681, 142679, 141289, 143214, 141860, 143378, 143099, 142264, 143652, 144984, 141909, 142204, 142351, 141849, 142607, 141384, 145086, 144900, 141084, 177378, 144933, 238578, 163375, 158151, 163150, 163334, 161481, 162665, 161590, 202754, 157032, 112902, 145826, 141991, 143879, 141211, 143747, 142783, 141707, 143558, 144982, 141944, 143850, 138849, 140792, 140439, 141253, 143548, 143139, 141768, 141687]
RT average latency: 150878ns
RT system stabilized
Initializing IO...
IO initialized
IO Ready signal sent to RT thread
RT system started and running
Received message: Response(Response { request_reference: 1, payload: Pong })
PONG
Received message: Response(Response { request_reference: 2, payload: Pong })
PONG
Received message: Response(Response { request_reference: 3, payload: Pong })
PONG
Received message: Response(Response { request_reference: 4, payload: Pong })
PONG
Received message: Response(Response { request_reference: 5, payload: Pong })
PONG
Received message: Response(Response { request_reference: 6, payload: Pong })
PONG
Received message: Response(Response { request_reference: 7, payload: Pong })
PONG
Received message: Response(Response { request_reference: 8, payload: Pong })
PONG
Received message: Response(Response { request_reference: 9, payload: Pong })
PONG
Received message: Response(Response { request_reference: 10, payload: Pong })
PONG
Received message: Response(Response { request_reference: 11, payload: Pong })
PONG
Received message: Response(Response { request_reference: 12, payload: Pong })
PONG
RT thread result: Ok(11606)
RT system stopped
```

## Links

Please subscribe to be notified of live-stream events so you can follow the development process.

* Patreon: https://www.patreon.com/MakerPnP
* Source: https://github.com/MakerPnP
* Discord: https://discord.gg/ffwj5rKZuf
* YouTube: https://www.youtube.com/@MakerPnP
* X/Twitter: https://x.com/MakerPicknPlace

## Authors

* Dominic Clifton - Project founder and primary maintainer.

## License

Apache 2.0 or MIT

## Contributing

If you'd like to contribute, please raise an issue or a PR on the github issue tracker, work-in-progress PRs are fine
to let us know you're working on something, and/or visit the discord server.  See the ![Links](#links) section above.