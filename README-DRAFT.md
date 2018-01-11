[ Concept layout and readme still a WIP. Further clarification, diagrams, are required. ]

                                    ICRE
                Integrated Circuit Reverse Engineering Framework

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

-------------------------------------------------------------------------------

                                Core Modules

  - Workflow UI

    KiCAD-like workflow UI [what is a KiCAD-like workflow?]. Needs to be
    intuitive to use via command line as well as graphically.

  - Imaging

    - Microscope control interface [what is this?]
    - Image preprocessing and quality verification 
    - Stitching

  - Netlist extraction

    This is where the research behind degate comes in. More to be written about
    this soon. 

  - Flowgraph componenet visualizer

  - 


-------------------------------------------------------------------------------

                          Principles of development

  - Modularity

    ICRE has to be extremely pluggable and easy to develop modules for. This is
    due to the vastness of the project, variety of chip imaging styles, image
    qualities, and chip types. In addition, well defined modularity enables
    accelerated research into various processes involved without having to
    re-invent the wheel.

    Core modules will go through a curation process for code quality, through
    the remaining core principles.

    Contribution repositories can be made for experimental plugins and non-curated
    code, to ease development and expand the project further than initially
    intended.

  - Standards development, adherence, and code documentation

    Because of the pool of research and image processes being used in ICRE,
    there has to be a set of standards to help the parts connect to each other, to
    help researchers make progress, and accelerate development of modules.

    For example, it would be good to make a spec for chip imaging formats and
    delayering information [unclear what this looks like].

    All parts of ICRE must be well documented, and the documentation must
    follow code as changes are introduced.

  - Reliability

    Bugs in the workflow will quickly result in a loss of interest in ICRE,
    giving marketing power to proprietary solutions. ICRE must have a thorough test
    suite to mitigate bugs and ease introduction of new developers.

  - Build on existing research

    There's already a few years worth of research and FOSS code that can be
    reused. Adopting existing code into ICRE does not only save development time,
    we also end up contributing improvements back to existing projects.

    For example, degate already implements planar silicon netlist extraction
    and workflows to quickly assist the image recognition process. By adopting the
    code, making the build process more reliable, and reworking it into a library
    framework -- we can make it easier to make improvements to the core
    functionality of the software.
    
    Other projects, such as Dr. Zonenberg's netlist to verilog IR research,
    are in need of image processing and netlist extraction frontends. ICRE should
    essentially connect various research together and fill in the gaps.

-------------------------------------------------------------------------------

                               Hard problems




-------------------------------------------------------------------------------
