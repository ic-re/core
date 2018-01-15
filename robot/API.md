ICRE-robot API Specification
----------------------------

ICRE-robot is an ICRE core module for controlling robotics related to the
decapping, imaging, laser, and micropositioner processes.

Scripts can be made to incorporate ICRE-robot into a GUI, a scriptable
environment that can be shared with other researchers, or routines for
calibration.

For example, a GUI can be made to incorporate ICRE-robot, ICRE-vision, and
ICRE-ui-control to provide a joystick control interface with a real-time view
of the microscope camera, with real-time analysis tests to ensure that each
tile is properly imaged for netlist extraction.

Parameters for motors, drivers, and controllers must be trivial to serialize
and de-serialize.
 
Interface lambdas are included for talking via UART, SPI, and PWM. 3rd party
plugins for interface lambdas can be implemented to ease introduction of new
controllers. [ Maybe reconsider this ]

Exposed functions / structures
------------------------------

    ToC                      Completion
    ---                      ----------
    1. Master Controller     0%
    2. |-- Sensor            0%
    3. |-- Controller        10%
    4.     |-- Driver        10%
    5.         |-- Stepper   10%
    6.         |-- Pump      0%
    7.         |-- Drill     0%
    8.         |-- Relay     0%
    9.         |-- Vibrator  0%


### 4. Driver
Work in progress...

### 5. Stepper

A stepper mainly consists of a dictionary of parameters, defining the physical
paramters of the stepper / body combination. The goal here is to create a
simple way to convert motor and [stage] body specification sheets, and even
infer parameters experimentally, into a unified interface for use with the rest
of ICRE's components.

The use of such information is dependent on the setup. If using a hardware
controller, many of these details may be ignored but still used to verify
correctness.

All units are SI meters, defined as Python floats.
[ A fixed type must be defined ]

The stepper object is defined as such:

    # Let's give some basic info on the object.

    Stepper.info = {
                     "Name"         : string,
                     "Description"  : string,
                     "Version"      : string,
                     "Author"       : string
                   }

    # Define the parameters of the stepper itself, regardless of body or
    # application.

    Stepper.stepper_spec = { 
                             # Degrees per notch. Dictates achievable precision
                             # without microstepping. Usually drivers will move
                             # the stepper at this rotation per pulse.
                             # Usually 0.72 or 0.31 degrees.
                             "Degree / Notch"        : float,

                             # Supported microstepping granularity. Allows
                             "Microstepping Divisor" : float,

                             # This ensures that the driver phase configuration
                             # matches the stepper specification
                             "Phase Count"           : int,

                             # Speed range the motor is speced for. I don't
                             # know of a case where a stepper can't drive
                             # backwards at the same rate as forwards, but
                             # implementing this as a range, anyway.
                             # [should be thought of as number of pulse / time]
                             "Velocity Range"        : (float, float)
                           }

    # Define the parameters of the body. Templates are provided for verious
    # applications: stage-horizontal (X or Y), stage-tilt (alpha or beta),
    # stage-rotation (theta), stage-z (Z), laser-horizontal (X or Y),
    # microprobe-horizontal (X or Y), microprobe-z (Z).

    Stepper.body_spec    = { 
                             # Supported linear range on axis, in meters.
                             "Travel Range" : (float, float),

                             # Maximum backlash
                             "Backlash"   : float          
                           }

If any sensing must be made at initialization for calibration, then it's
acceptable to call a function in place of a value -- but please make it obvious
in the console printout if you choose to do so.

ICRE should work with the least amount of provided information. Additional information can be used for error adjustment and callibration.

However, to improve accuracy, error detection / adjustment routines, more
information can be given by the motor specification. These parameters are
optional, but can improve reliability and reproducability of the system.
One must derive these values from the motor specification and/or through
specification.

Several templates are provided for various stepper motor + stage
configurations.

