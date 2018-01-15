[ Concept layout and readme still a WIP. Further clarification, diagrams, are required. ]

# ICRE-CORE
### Integrated Circuit Reverse Engineering Framework

ICRE is an open source silicon auto-analysis framework. If you are a software
reverse engineer, then ICRE is the radare2 + GDB of silicon. ICRE can be used
to aid analysis of a microchip, produce IR code [from what?] which can be
converted to human readable verilog, convert a netlist into a transistor level
simulation, or into a QEMU module for test development.

ICRE is designed to be modular and pluggable for a wide variety of imaging
processes and outputs. The work done so far is preliminary, and requires
specialized work from a wide variety of fields -- computer vision, VLSI and HDL
(building as well as reverse engineering), and talent in building scalable,
stable software. Furthermore, volunteers can contribute ASIC kit and IP data
into a repository, that can then be re-used when analyzing new chips, speeding
up the reversing process.

If this sounds interesting to you, then join us at #icre on freenode.

Core Modules
------------

All modules are standalone libraries, which follow a carefully documented API
specification. Each of these modules should be daemonizable, API calls and
arguments should be serializable for network transport.

  - ICRE-ui

    KiCAD-like workflow UI [what is a KiCAD-like workflow?]. Needs to be
    intuitive to use via command line as well as graphically.

  - ICRE-ui-control

    Live control interface for ICRE-robot. Here, it is implemented as a pygame
    interface, with submodules for interacting with joysticks.

  - ICRE-script

    Scriptable control interface for ICRE components. 

  - ICRE-robot

    - Control interface for microscope (X, Y, Z, A, B, T),
      Laser (X, Y, Power),
      Motorized microprobe / micropositioner (X, Y, Z).

    - Intended to be used with ICRE-vision and ICRE-ui-control.

    - Instead of ICRE-ui-control, can be issued control commands
      directly or via the ICRE-script.

    - Exposes a generic sensor interface, which is currently used to
      keep track of stepper motor state (or query it from the stepper
      controller, if there is one).

    - Command primatives should be kept simple, in order to implement
      ICRE-robot cheaply on a microcontroller.

  - ICRE-vision

    Exposes primitives to help with the chip imaging process, i.e. a stitcher,
    some hough line stuff for making sure tiles are good quality, and so on.

    Run cv models to extract useful information about the image.

    [ I think it makes sense to merge ICRE-vision and ICRE-degate. ]

    - Image preprocessing and quality verification 
      - This gets run against every captured tile, and trace connectivity
        gets tested as more tiles are captured.

    - Stitching

    ( template matching based on normalized cross-correlation )

  - ICRE-degate

    This is where the research behind degate comes in. More to be written about
    this soon. 

    Netlist to gate array

  - ICER-flowgen

    Flowgraph componenet visualizer

  - ICRE-vloggen

    Gate array to verilog

  - ICRE-qemugen

    Gate array (or verilog?) to qemu module

  - ICRE-simulate

