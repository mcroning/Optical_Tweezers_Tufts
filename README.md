# Optical_Tweezers_Tufts
LabVIEW code for running optical tweezer based rheology setup
This repository contains the source distribution for the labview program that currently runs the optical tweezers setup in lab 211 at Tufts Sci Tech Center, 4 Colby Street, Medford MA 02155

It contains a main loop driving the microscope camera, receiving data from the QPD and a rudimentary feedback loop to try to stabilize the trapping beam on the trapped bead. The Thorlabs Kinesis Cube can probably do this better by itself.

There is another loop to handle events such as mouse calibration, mouse motion to steer the beam, set lock-in frequency, change beam focus update PID parameters, record and write lock-in data. A third loop handles the temperature PID loop for sample temperature control.

Optical tweezers setup details

Room 211

The main laser is a 980 nm fiber coupled diode laser, powered by a Newport Model 8000 power supply. The laser is fiber coupled and collimated by a 40x objective lens. I generally set the laser temperature to 20o C and power to less than 200mW.  10mW is often plenty.  The NIR beam is then combined with a HeNe 633nm beam at a dichroic mirror. This visible HeNe beam is used to assist alignment and to provide a constant power beam for the quadrant photodiode position detector. It can be switched on and off using the provided electronic shutter. A variable neutral density filter wheel is placed just after the shutter to provide attenuation as needed.   A Toptica 488nm laser diode beam can also be switched in using a flipper mirror. There are two adjustable irises in the beam train to help with making the beams colinear. A beam raiser elevates the beam(s) for the relay lenses and the beam steering galvanometers. The relay lenses image the beam steering mirrors onto the back aperture of the trapping objective lens. The trapping/imaging objectives are designed for 160mm tube length and are not infinity corrected. Therefore, the relay optics focus the trapping beam in the back image plane of the objectives, several centimeters behind them.  The trapping beams are reflected to the vertical by a dichroic which reflects NIR but passes shorter wavelengths This allows the microscope’s white light illumination to pass through to the microscope imaging camera (a high speed (750fps) Basler Ace). The trapping objective is mounted on a piezoelectrically adjustable mount to allow computerized focus control. Another objective is used as a condenser with the dual purpose of (1) focusing the white light source used to image the sample and (2) collimating the transmitted NIR trapping beam and red tracer beam for delivery to the quadrant photodiode (QPD) position sensor. A NIR blocking filter removes the residual trapping beam so that the QPD sees only the res HeNe beam. The QPD is monitored by a Thorlabs Kinesis position aligner. This position aligner can be used to provide feedback signals to the steering mirrors to keep the transmitted beam centered on the QPD if desired. 

The electronic breadboard on the KM laser hosts two circuits. One is an opamp-voltage adder that adds the steering voltages from the National Instruments DAQ board to a sinusoidally oscillating reference voltage from the SR 850 lock in amplifier. This causes a trapped bead to undergo sinusoidal oscillation about its mean position. The lock-in can then measure the amplitude and phase of the bead’s response to forced oscillation in its viscous surrounding medium to enable a measurement of the material’s viscoelastic properties. Simultaneously recorded video of the motion of the bead can be used to establish the trap stiffness (pN/micometer). The second circuit on the breadboard is for temperature control of the sample under test. The USB 6008 NI DAQ is used for thermistor-based temperature measurement, and to supply control voltages to a power op amp which drives heating current through a 10 Ohm heating resistor in the sample holder. (Home made from glass slides glued together.)

There are filters that can be placed in front of the camera to remove residual NIR and/or red laser light.
There is a second camera in the setup for a side experiment.  This Point Grey camera has been used to record the light passing through a distorting medium (e.g. multimode optical fiber) as the laser is scanned across the entrance face by the galvanometer mirrors. To use this setup the dichroic which usually reflects the laser beam vertically into the microscope is flipped out of the way. 

The Toptica laser uses a power supply, currently set up on the far side of the femtosecond laser. The laser can be controlled using the iBeam Smart GUI currently installed on the controller PC

Software:

Start the program ( main_tweezer_program) from Tweezers211_2020 labVIEW project.
The microscope camera image should immediately appear in the image frame. Load a sample on the inverted microscope, turn on the fiber optic microscope illuminator, and make sure that light is directed through the condenser objective.  In future it would be good to replace the fiber optic with a white LED. The sample should be then visible in the image frame. Open the electronic shutter to allow the red HeNe beam to pass. You may need to add the green filter in front of the camera to avoid saturating the camera. Adjust focus manually to focus the red beam on the glass coverslip so that it is reflected to the camera. Then click the calibrate mouse button on the lower left of the instrument. Click on the image of the image of the focused beam in the image frame. The focused beam will jump to a new position.  Click on the new focus position in the image. The beam will jump again. Click on the second new position. The beam steering is now calibrated and the beam will follow the mouse cursor. The beam can be stopped from moving with the mouse by toggling.

Controls:

Period: Imaging loop cycle time in milliseconds. This is the time between data lock-in QPD data points.
Set Frequency: Lock in amplifier reference frequency and hence bead oscillation frequency
Focus out: voltage applied to piezo objective holder. Typical range 0 to 1 volt
Focus Increment: change in focus voltage with each click of focus out control
Temp setpoint: Desired sample temperature. (When temp controlled ample holder is used)
Response magnitude and phase: instantaneous reading from lock-in
Mean Magnitude and Phase: 100 point average of lock-in magnitude and phase

Tabs:
Camera:	
  Exposure time LS: exposure time in microseconds set when program starts
  Exposure time LS while run: control to adjust exposure time while program is running 25000 is good starting     point for 100x objective.
  Number of images: not used

Tracking: 
 Used in older version of software for particle tracking.

Temp PID:
  For sample temperature controller. Should not need adjustment. If needed the gains can be autotuned

Bead focus track:
  This section is under development. The aim will be to have the trapping laser lock onto the bead. When the trapping beam is oscillating, the average position of the beam should lock onto the center of the bead.

K Cube PID: Also under development for same purpose as the software based beam stabilizer under bead focus track above.
Data Writer:
Record Data: store current oscillation frequency, and mean magnitude and phase of bead response at that frequency, and sample temperature in array row
Write to file: Write excel spreadsheet of data recorded in array for later analysis.


