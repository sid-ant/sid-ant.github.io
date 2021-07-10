---
layout: post
title:  "Macbook Pro 16 is HOT!"
date:   2021-07-10 21:47:55 +0530
categories: tech
---

Macbook Pro 16 launched in 2019, with rave reviews from the entire tech lifestyle yoututers and several of the tech blogs. However, MBP 16 is one of the worst product, I've had the displeasure of using. Here's why. 

# You can not even connect a single external display 

The moment an external monitor is connected, both `temps` & `kernel_task` CPU consumption starts rising. Within 15 minutes of usage, the entire laptop becomes unresponsive. The laptop takes about 5 minutes to become responsive post disconnecting the external display. It's astonishing that a $2500 laptop, can not drive an external display. 

# Absense of multitasking even with the 6/8 core CPU 

At work, we have large codebases of `purescript` and `haskell`. Compilation on MBP chokes the entire system, the chassy becomes boiling hot and my productivity as the developer plumets. We can not share our screens or even attend a google meets call while compiling since the laptop simply can not multitask. 

# Laptop can not be used on Lap 

Macbook 16 chassy alwasy remains at a baseline temperature which is too uncomfortable to be put on your lap. 


# Why? 

This is not a new problem and there are already hunderds of forums explaining why this happens. 


## Intel i7-9750H / Turbo Boost ( 2.6Ghz to 4.5Ghz )

Our first major culprit is `Intel`. Intel rates this CPU's power consumption at 45W however due to the nature of `turbo-boost`, it would often consume upwards of 90W. Turbo Boost, overclocks the CPU for a short interval. The short interval is determined by the capacity of the machine to sustain the CPU temperatures below 99C. Once the terminal temperature is reached, the processor underclocks itself to cool itself down. 

While this looks like a reasonable enough strategy, I've observed that it results in a strange cycle where you never have a responsive system.

1. A demanding multi-threaded process is started. 
2. CPU overclocks itself to 4Ghz+ making the entire laptop unresponsive ( CPU utlization 100%)
3. Terminal Temprature is reached. 
4. To cool down, MacOS puts a dummy process `kernal_task`, processor starts to underclock. ( laptop is still unresponsive )
5. The laptop cools down just enough to overclock itself again. 
6. The cycle continues until the process is terminated.

### Solution

My personal laptop (MSI GF-65) is also configured with the same processor. Playing games with default turbo boost results in extremely high temperatures and jittery gaming experiance. Since the laptop runs Windows, I use a tool called `throtle-stop` to limit the power consumption of the CPU at 35W. I also decrease the max turbo limit to 3.5Ghz. Just these 2 steps result in a laptop whose CPU temps never go beyond 80C. Games then provide a consistent smooth performance, albeit with lesser maximum fps. 

I have done some more experiments with this processor and the results are: 

1. At 35W, all cores only reach 2.3Ghz. 
2. At 45W, all cores reach 2.6-2.8Ghz. ( Turbo boost is enabled but the processor is not allowed to consume more than 45W)
3. With no changes to power consumption, and turbo boost disabled, the all cores go up to 2.6Ghz and never beyond. 

In conclusion `Intel i7-9750H` provides a much better experiance with turbo boost disabled. I also dual boot ubuntu on this laptop, and I always disable turbo boost. 

MacOS Solution: Use `turbo-boost-switcher` by  http://tbswitcher.rugarciap.com/
The catch: Tool reqiures root privileges to work, which you may not always have in a work machine. Windows, comes with power mangement out of the box, where you can set the max the CPU consumption to 99% which also results in disabling on turbo boost. On windows, you can also set the max consumption to 30-40% to save battery. Sadly, MacOS does not have this feature. 

