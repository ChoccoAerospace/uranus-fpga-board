---
title: "uranus-fpga-board"
github: "https://github.com/ChoccoAerospace/uranus-fpga-board/tree/main"
description: "Found out about FPGAs and thought they were very cool—decided to try making a board for a nice one. Calling it Uranus because Uranus is a goated planet (YOOR-uh-nús)"
created_at: "2026-10-04"
total_time: "2.5h"
---

## October 4th, 2026
### FPGAs are Actually Pretty Hype

![Pinout of Xilinx Kintex 7 XC7K160T-2FFG676C](https://github.com/ChoccoAerospace/uranus-fpga-board/blob/main/Images/160Tpinout.jpg)

Okay, the most important part of an FPGA board is the FPGA, so what is it, exactly? An FPGA stands for "Field-Programmable Gate Array," and if you are like me, that provides no usable information. FPGAs are a type of Programmable Logic Device (PLD). Other PLDs, like CPLDs, typically have a coarser, simpler architecture than an FPGA. FPGAs use Hardware Description Languages (HDLs) to control how their many programmable logic blocks work with other blocks to perform functions. The Field Programmable part of an FPGA comes from how its wiring can change based on instructions from something written in an HDL, as opposed to an Application-Specific Integrated Circuit (ASIC) that cannot change its logic wiring. FPGAs are often used to prototype before going all in on production of an ASIC. In my case, I am using an FPGA because I want to be able to change it to whatever I want and don't want to order a huge load of ASICs. An FPGA is NOT a microcontroller, but you can describe its hardware (lol) to make it work like a microcontroller, or even a processor.

**What makes an FPGA board a Tier 2 project, offering $250 in grant funding?**  
While putting this in the same tier as a robot arm, handheld console, or battle bot might seem strange, as the others have far more physical possibilities and polish (maybe), an FPGA board is very complex and requires precise PCB design. FPGAs often require several different voltages, and they have so many pins that a 4- or 6-layer PCB is necessary, as well as DDR RAM if you want storage that is slightly longer than the BRAM. Obviously, there is more, but I don't know enough.

**What FPGA will I use on my board?**  
Uhhhhh idk yet, but I have a good idea. I want to be able to do some cool stuff with electricity and lots of data, so I want something on the higher end of the speed scale. I think I would get a Xilinx Kintex-7 XC7K70T-2FBG676C or XC7K160T-2FFG676C. The former is about $35, and the latter is more like $80. If I can find a way to level up this board to Tier 1, I may go even further because I think that sounds cool.

**Other stuff that would probably go on the board**  
RAM, I haven't researched enough about RAM yet. Capacitors, lots of them. JTAG adapter. Ports going out to connect with other devices. Headers, if I want to connect another module directly if I fear the cables. Lots of power stuff and regulators. Clock generators. Buttons and LEDs.

I intend to supply power to this board with a bench power supply (OOH, I could make that!), so it doesn't require an extreme amount of power thingamabobs, just enough to handle the power degradation from traveling over a cable.

**Total time spent: 2h**

___

### Brainthinks from the same day

![Mezzanine connector](https://github.com/ChoccoAerospace/uranus-fpga-board/blob/main/Images/mezzanine.jpeg)

I don't think headers would be the best to preserve signal integrity. Upon doing more research, it sounds like edge connectors or mezzanine connectors will be the best. Both for signals and power. Edge connectors put the card at a 90-degree angle, while mezzanine connectors put it parallel. I think a mezzanine connector would be better. Even for power, the large number of pins on a mezzanine connector helps reduce power quality degradation by lowering parasitic inductance, canceling out the magnetic field (if PWR and GND are alternated), and having a large cumulative surface area. Surface area is important because, while power will be sent as DC, the FPGA will pull power in very fast, erratic pulses, creating noise. I will have a mezzanine connector for both power and a peripheral board for testing.

**Total time spent: 0.5h**
