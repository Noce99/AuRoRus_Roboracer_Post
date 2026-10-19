# AuRoRus: our RoboRacer race stack, open-sourced and written in Rust

What if I told you that the following is just a few terminal commands away from you?

![The AuRoRus web GUI simulating the Frenet overtaking against the MPC on the Vienna 2026 qualifying track, with their lateral errors plotted below](./assets/frenet_overtaking_vs_mpc_simulating_to_race_at_vienna_quali.gif)

*Our two race algorithms, Frenet overtaking and MPC, racing each other in simulation on the ICRA 2026 Vienna qualifying track.*

No containers, no system dependencies, no workspace juggling: one `cargo build` and you're done. [Try it](https://github.com/Noce99/AuRoRus):

```sh
# install Rust, then load it into the current shell:
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
. "$HOME/.cargo/env"
# get the code and build it:
git clone https://github.com/Noce99/AuRoRus && cd AuRoRus
cargo build --release
./target/release/web_gui
# then open http://localhost:1999
```

My name is Enrico Mannocci. I'm a third-year PhD student, and I have been the leader of the University of Bologna 1:10 Scale Driverless division since 2024. After winning the RoboRacer competition at ICRA 2025 in Atlanta, and taking second and third place with our two cars at ICRA 2026 in Vienna, we are ready to open-source our race stack for everyone.
In this post I will present AuRoRus: an independent autonomous RoboRacer stack whose every node is written in Rust (ROS 2-free).

## First of all: why are you running away from ROS 2?

ROS 2 is a great tool, but it's too generic. That's fine: I don't expect anything else from software called Robot Operating System. But by using it you accept a comfort zone that you pay for with efficiency and with tons of features you don't really use (like DDS discovery traffic, which is a common cause of connection drops over the congested Wi-Fi of a race area). That said, I really like the ROS 2 topic-node paradigm, and I ported it into AuRoRus.

## Second: why Rust?

Rust is a really pedantic, slow-to-write language that gets you very close to the old-fashioned programmer's dream of "if it compiles, it works". It also executes extremely fast, totally [comparable](https://programming-language-benchmarks.vercel.app/c-vs-rust) with the evergreen C, but with much easier-to-understand compiler errors (and readable runtime panics too). It has a very mature package manager, **cargo**, that lets you compile other people's code with very little effort. Everything is amazing, but the "really pedantic, slow-to-write language" part is still there... or maybe not? What if an efficient Rust backbone that shares information between nodes, lets you see everything live and lets you debug in detail was already there, and you just needed to write the important code? That's what AuRoRus is.

## Why a web GUI? Isn't it too slow?

It's the best way to see what is really happening on our cars, and I did my best to keep it as resource-light as possible. The page is plain HTML, CSS and JavaScript, with no framework and no build step, and it is compiled into the binary, so there is nothing to deploy. It polls the car at a rate you choose, from 1 to 100 Hz (30 Hz by default), so you can turn it down on a slow connection. It's also completely removable: it's just a node like all the others, and you can turn it off and run the whole stack without it.

## Why now?

I started thinking about porting our ROS 2 repo to Rust two years ago, but I had the ideas and no time to implement them. AI-assisted development let me build this repo over the summer. I did my best to keep the code clean, documented, well written and, most importantly, easy for humans to extend. LLMs are good at writing boring code, but I believe the really important parts of autonomous racing need to be written by humans to be effective.

## What can I do with AuRoRus?

You can simulate, or run on real hardware, every part of a RoboRacer race or test session. More precisely, you can:
1) Calibrate your hardware
2) Map a new track
3) Localize the vehicle on a previously mapped track
4) Plan a race line on a map
5) Run reactive control algorithms
6) Run path-following algorithms with overtaking strategies
7) Benchmark different control algorithms and compare them in detail
8) Record debug sessions and replay them step by step
9) Record mapping sessions to fine-tune the mapping
10) Run your whole stack with minimal laptop-car communication in RF-congested environments such as race venues

## Supported hardware

AuRoRus drives the real car through these drivers:
- **Motor controller:** VESC 6 MkV over USB serial, which also provides the IMU
- **LiDAR:** Hokuyo UTM-30LX-EW, or any Hokuyo speaking SCIP 2.0 over Ethernet
- **Gamepad:** tested with wireless dongle gamepads

The onboard computer just needs to run Linux. Every driver can be tested on its own with the `probe` tool, and `car_calibration` guides you through calibrating a new car. If your car uses different hardware, a new driver is just another node.

## Is AuRoRus for beginners?

Absolutely, yes. I don't know an easier way into the RoboRacer world. This is actually the real motivation behind this software: too many beginner students were quitting our autonomous driving group early after struggling for hours to get the whole ROS 2 pipeline working on their laptops.

## Conclusion

Can't wait to see you in Seoul at ICRA 2027. Well, I hope so: it would mean I found the money to bring our team to the RoboRacer race again. If you'd like to help us get to Seoul, reach out! Good luck with the new season, enjoy [AuRoRus](https://github.com/Noce99/AuRoRus) (dual-licensed MIT/Apache-2.0), and if you like the project, don't hesitate to open a pull request with your algorithms.
