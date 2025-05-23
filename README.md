# PET-Digital-Simulation

## About

This is an (almost) complete logic-level simulation of the Commodore PET Computer using the [Digital](https://github.com/hneemann/Digital) logic circuit simulator.

It is based on the original schematics which are recreated page by page.

![overview](./docs/images/full_system_booted.png)

## Requirements

To run this simulation the Digital Simulator by Helmut Neemann is required. It can be downloaded [here](https://github.com/hneemann/Digital/releases/latest/download/Digital.zip).

After starting Digital a Plugin containing the simulation code for the 6502 CPU and some other special chips needs to be loaded into Digital.
Go to `Edit`->`Settings`->`Advanced`->`Java Library` and select the "PETComponentsDigitalPlugin.jar" file which is included in the PET Simulator.

After adding the plugin a restart is required.

## Starting the Simulation

From Digital open the file `Mainboard.dig`.

The simulation can be started immediately by pressing the ▶ button on the upper toolbar.

The speed of the simulation can be controlled by the 16MHz Clock Component in the DEBUG frame.
![Clock Element](./docs/images/clock_element.png)

A right click opens a dialog box where the simulated speed can be selected.
Deselect the `Start real time clock` checkmark to step through the simulation cycle-by-cycle by repeatedly clicking on the clock element.

In this mode it is also possible to set breakpoints on signals and run the simulation until a breakpoint is hit.

Caveat: If you cannot find the Keyboard Input dialog box, it is probably hidden behind the screen output dialog.

Further information on how to use the Digital Simulator can be found in its documentation (`HELP`->`Documentation`)

## Why?

This project was started after watching this [youtube video](https://www.youtube.com/watch?v=nxilekpLp6g) by [curiousmarc](https://www.youtube.com/@CuriousMarc), where he and [Ken Shirriff](https://www.righto.com/) repair a broken PET2001.

To follow the repairs I looked at the PET schematics - but got the wrong schematics. In the video they repair an original PET with static memory, not the dynamic memory in my schematic.

But as I have always been curious about how dynamic RAM works, especially the refresh part, I decided to simulate the memory part to see how it works.

Once that was running in the simulator I was intrigued by the video circuit. Having started in computing with the VIC20, I had wondered how video was generated before the advent of dedicated video chips.

After the video circuit was working and generating a valid image the decision was made to just implement the whole system and see if it can boot.

Which it can 😊

## PET Version

This simulation replicates the PET2001N-16, also known as the "dynamic PET". In Europe this version was sold as the CBM3016.

This version was chosen because, unlike the original PET, it uses dynamic RAM and, unlike the later 4000 and 8000 Series, the video output is generated only with conventional 74-series logic chips and not with a boring dedicated video controller chip.

This PET version runs BASIC V2.  
AFAIK the later BASIC versions require the video controller and cannot be used.

## Speed

This simulation currently has about 570 logic elements, whose state needs to be calculated multiple times for every change of the main clock signal (a 16 MHz clock) as the signals propagate through them.
Additionally there are the screen updates which happen multiple times a second.

In other words this simulation is slow and far from running in realtime.

On my development machine (a few years old Core i7-8565U @ 1.80 GHz) the simulation runs at about 120 kHz (120.000 cycles of the 16MHz clock per second) resulting in about 0.75% or 1/133th of the original speed.

So trying to run anything on the simulated PET requires quite a bit of patience. Even getting to the BASIC ready prompt takes about 2 minutes.

The speed could be improved a bit by dropping schematics accuracy and replacing components with faster substitutes - e.g. replacing the 16 RAM chips with a single RAM simulation. But the goal of this simulation is not speed but signal accuracy 😊

## Compatibility

The simulated system is fairly compatible with the real PET.

It can run the TIM (Terminal Interface Monitor) by executing
> SYS1024

![TIM](./docs/images/TIM.png)

It can change to lowercase letters with
> POKE59468,14

![Lowercase](./docs/images/poke59468.png)

And it contains the Microsoft easter egg 😁
![Microsoft Easter Egg](./docs/images/microsoft_easter_egg.png)

## Bugs

The simulation has some known bugs:

- About 50% of the time the simulation boots into the TIM monitor program instead of BASIC. The cause of this is unknown and hard to debug as it is non-deterministic (Digital has the "feature" of setting a random initial value for Flip-Flops and Hi-Z outputs)

- Connecting the DO (Data Output) pins of the upper 16k RAM bank to corresponding pins of the lower bank causes spurious short circuits which will stop the simulation. The problem probably lies somewhere within the simulated RAM logic. This is currently fixed by disconnecting the DO pins of the upper bank. This also reduces boot time by about 2 minutes as the Kernal RAM check only takes half as long.

- Writing to cassette tape does not work. The CASS WRITE line is constantly high.

- The IEEE-488 Interface is not implemented. While this could be added reasonably easy, some kind of simulated IEEE-488 device would be required to make the effort worthwhile. And that part is definitely non-trivial.

## TODOs

- Fix the Bugs
- Maybe add a simulated cassette drive to save and load programs.
- Implement the 4116 RAM chips with a custom component to make them faster and more reliable.
- Some other interesting systems like the Apple 1
