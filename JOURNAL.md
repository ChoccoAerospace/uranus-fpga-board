---
title: "uranus-fpga-board"
github: "https://github.com/ChoccoAerospace/uranus-fpga-board/tree/main"
description: "Found out about FPGAs and thought they were very cool—decided to try making a board for a nice one. Calling it Uranus because Uranus is a goated planet (YOOR-uh-nús)"
created_at: "2026-10-04"
total_time: "11h 50m"
---

# October 4, 2026: FPGAs are Actually Pretty Hype
<!-- fabricate:entry 138 -->

![Pinout of Xilinx Kintex 7 XC7K160T-2FFG676C](https://github.com/Silllies/uranus-fpga-board/blob/main/images/160Tpinout.jpg)

Okay, the most important part of an FPGA board is the FPGA, so what is it, exactly? An FPGA stands for "Field-Programmable Gate Array," and if you are like me, that provides no usable information. FPGAs are a type of Programmable Logic Device (PLD). Other PLDs, like CPLDs, typically have a coarser, simpler architecture than an FPGA. FPGAs use Hardware Description Languages (HDLs) to control how their many programmable logic blocks work with other blocks to perform functions. The Field Programmable part of an FPGA comes from how its wiring can change based on instructions from something written in an HDL, as opposed to an Application-Specific Integrated Circuit (ASIC) that cannot change its logic wiring. FPGAs are often used to prototype before going all in on production of an ASIC. In my case, I am using an FPGA because I want to be able to change it to whatever I want and don't want to order a huge load of ASICs. An FPGA is NOT a microcontroller, but you can describe its hardware (lol) to make it work like a microcontroller, or even a processor.

**What makes an FPGA board a Tier 2 project, offering $250 in grant funding?**  
While putting this in the same tier as a robot arm, handheld console, or battle bot might seem strange, as the others have far more physical possibilities and polish (maybe), an FPGA board is very complex and requires precise PCB design. FPGAs often require several different voltages, and they have so many pins that a 4- or 6-layer PCB is necessary, as well as DDR RAM if you want storage that is slightly longer than the BRAM. Obviously, there is more, but I don't know enough.

**What FPGA will I use on my board?**  
Uhhhhh idk yet, but I have a good idea. I want to be able to do some cool stuff with electricity and lots of data, so I want something on the higher end of the speed scale. I think I would get a Xilinx Kintex-7 XC7K70T-2FBG676C or XC7K160T-2FFG676C. The former is about $35, and the latter is more like $80. If I can find a way to level up this board to Tier 1, I may go even further because I think that sounds cool.

**Other stuff that would probably go on the board**  
RAM, I haven't researched enough about RAM yet. Capacitors, lots of them. JTAG adapter. Ports going out to connect with other devices. Headers, if I want to connect another module directly if I fear the cables. Lots of power stuff and regulators. Clock generators. Buttons and LEDs.

I intend to supply power to this board with a bench power supply (OOH, I could make that!), so it doesn't require an extreme amount of power thingamabobs, just enough to handle the power degradation from traveling over a cable.

___

## Brainthinks from the same day

![Mezzanine connector](https://github.com/Silllies/uranus-fpga-board/blob/main/images/mezzanine.jpeg)

I don't think headers would be the best to preserve signal integrity. Upon doing more research, it sounds like edge connectors or mezzanine connectors will be the best. Both for signals and power. Edge connectors put the card at a 90-degree angle, while mezzanine connectors put it parallel. I think a mezzanine connector would be better, even for power. The large number of pins on a mezzanine connector helps reduce power quality degradation by lowering parasitic inductance, canceling out the magnetic field (if PWR and GND are alternated), and having a large cumulative surface area. Surface area is important because, while power will be sent as DC, the FPGA will pull power in very fast, erratic pulses, creating AC noise. I will have a mezzanine connector for both power and a peripheral board for testing.

**Total time spent: 2h 30m**

___

# October 5, 2026: That's, ummmm, a lot of pins
<!-- fabricate:entry 152 -->

![Schematic of the previously mentioned Kintex 7 160T chip](https://github.com/Silllies/uranus-fpga-board/blob/main/images/kintexSchematic.png)

I mean I did say that PCB design is comforting, but that was with a simple board that connects some preassembled boards. Now I have to learn what all these pins mean.

Okay, I did some more research and have decided that this project likely belongs in Tier 1. An FPGA board is provided as a Tier 2 example for simpler FPGAs, but I am using a far more complex FPGA, as well as DDR RAM. A similar FPGA board from Blueprint that also had RAM was rated as Tier 1. I also did some more research on the processor and found a better and cheaper model! The XC7K160T-3FFG676E is faster (Speed grade 3 instead of 2) and has a higher maximum operating temperature (E has a max of 100 degrees while C maxes out at 85), and LCSC sells it for $73.50, as opposed to $96 for the other. I don't really need the 676 ball package, but the 484 version doesn't have an equivalent sold by LCSC.

NEVERMIND! LCSC sells an XC7K325T-3FFG900E for nearly the same price! I do not need this, but why not pay the same price for something FAR better! Now I have to redesign my schematic (At least where I got to) and get less sleep (I need more sleep; it's Klausur season)

Okay, there are a lot of power lines. I don't understand it all, but there are several voltages the chip takes. VCCO pins can take many voltages, depending on the interface. There is also a lot of stuff for the GTX transceivers, which I also don't fully get. I haven't gotten to labelling all the IO pins yet, (which is more than the 646-ball). I did route the GND, though!

![Schematic of the 325T](https://github.com/Silllies/uranus-fpga-board/blob/main/images/325Tschematic.png)

**Total time spent: 3h 20m**

___

# October 6, 2026: RAMpocalypse
<!-- fabricate:entry 167 -->

![RAM chip](https://github.com/Silllies/uranus-fpga-board/blob/main/images/W632GU6NB-11.png)

Found some RAM I am fine with using. 4 chips of 16 bit DDR3L 933 MHz. Each chip is $11, which I find quite insane. $11 is also the lowest price I found during my searching. The chip is the Winbon W632GU6NB-11, sourced from LCSC, obviously. I think I will use Aisler as they are based in Europe, have a minimum assembly count of 1 (I believe), and can source their parts from LCSC. I will probably see if they can pre-order the FPGA and hold it for me as I design it, as there is only 90 left. I will also have to ask on slack. Parts and manufacture will probably be more expensive, but it will be cheaper than assembling 2 boards from JLCPCB.

I added the RAM to the schematic, routed grounds, and am currently waiting for Vivado to download so that I can use MIG to handle the DDR3 controller. I am doing this now because it also tells what pins I should I use out of the 900 I have to choose from :3

I learned that 16 bit DDR3 chips separate half the bits into "upper" and half into "lower" bits. This is because the 16 bit chip is structured as two 8 bit slices. The signals alternate between the two slices, controlled by upper and lower data strobe differential pairs.

Finished schematicizing (???) the 325T and the 4 RAM chips. I initially tried to make it look nice, but the sheer volume of connections decided that would not happen. I know there is a way to make the schematic not as complicated and reducing connections, but I don't really want to mess with that. Yes I did actually spend 6 hours doing this; of course, not in one sitting. Maybe like 2 or 3. I used MIG to generate the memory interface stuffs, which does include the wiring, which is how I put everything together (and why the connections could seem random). I am dead tired now and there will be tea to wake up to from my rocketry club back home. goodnite!

![Wacky schematic](https://github.com/Silllies/uranus-fpga-board/blob/main/images/325TnRamSchem.png)

**Total time spent: 6h**
