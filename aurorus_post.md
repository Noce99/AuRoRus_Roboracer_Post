What if I tell you that this:

is 3 terminal command away from you. No containers, no tedious source compilation, just ready to be used in few minutes.

My name is Enrico Mannocci, I'm a third year PhD and I have been the University of Bologna 1:10 Scale Driverless division leader since 2024. After having won the Roboracer ICRA 2025 competition in Atlanta and got the third and second place at ICRA 2026 in Vienna we are ready to open to every one our race stack. 
In this post I will present AuRoRus: an indipendent Autonomous Roboracer stack written entirely in Rust (ROS2 Free).

First of all: why are you running away from ROS2?
ROS2 is a grate tool but it's too generic. I mean it's ok, I do not expect anything else from a software called Robotic Operative System but using it you are accepting a comfort zone that you pay with efficiency and tons of stuff that you are not really using (connection problems in electromagnetic dense race areas). This stated I really like the ROS2 topic-nodes paradigm and I ported it into AuRoRus.

Second of all: Why Rust?
Rust is a really pedant and slow to write language that get you really close to the "if it compiles it runs" old fashion programmer dream. It's also extremely fast and it's totally [comparable](https://programming-language-benchmarks.vercel.app/c-vs-rust) with the evergreen C but with extremely easier to understand compilation (and if you really try to execution) errors. It has an extremely mature package manager: **cargo** that let you compile other people code with really small effort. Everything amazing but "really pedant and slow to write language" is still there, or maybe not? What if an efficient Rust backbone that takes case of sharing information between nodes, let you see live and let you debug finely is already there and you just need to write the important code: AuRoRus is this.

Why a WebGui isn't it slow?
I tried my best to let it be as resource light as possible and it's completely removable, it's just a node as all the others and can just be quitted to run all the stack without.

Why now?
I started thinking about a porting in Rust of our ROS2 repo 2 years ago but I was having good ideas but not the time to implement them, vibecoding let me produce this report during summer.