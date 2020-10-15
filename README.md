# Optical_Tweezers_Tufts
Labview code for running optical tweezer based rheology setup
This repository contains the source distribution for the labview program that currently runs the optical tweezers setup in lab 211 at Tufts Sci Tech Center, 4 Colby Street, Medford MA 02155

It contains a main loop driving the microscope camera, receiving data from the QPD and a rudimentary feedback loop to try to stabilize the trapping beam on the trapped bead. ALthough the Kinesis Cube can probably do this better by itself.

There is another loop to handle events such as mouse calibration, mouse motion to steer the beam, set lock-in frequency, change beam focus update PID parameters, record and write lock-in data. A third loop handles the temperature PID loop for sample temperature control.
