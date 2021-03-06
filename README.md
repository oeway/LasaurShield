
The LasaurShield is a custom PCB for the [Lasersaur project](http://lasersaur.com). It's an [Arduino](http://arduino.cc/) [shield](http://arduino.cc/en/Main/ArduinoShields) that connects laser, stepper, stepper driver, stepper power, limit switches, door sensor, water chiller sensor, emergency stop sensor, and Arduino. Additionally core safety functions are also hardwired on the board (logic gates). The laser is forced off when any of the following occurs: door opens, chiller off or malfunctions, a limit switch triggers.

The LasaurShield is designed around the SparkFun Eagle Library, their design and CAM job rules. Check out the [SparkFun Tutorial](http://www.sparkfun.com/tutorials/108) if you are new to this. If you are interesting doing your own production run check out [this tutorial](http://www.sparkfun.com/tutorials/109).


The following Eagle library and design files are being used:

- cam/sparkfun-gerb274x.cam
- dru/LasaurShield.dru
- lbr/[SparkFun.lbr]
- lbr/con-phoenix-254.lbr (comes with Eagle)
- lbr/con-phoenix-508.lbr (comes with Eagle)
- lbr/con-weidmueller-sl35.lbr (comes with Eagle)


**DISCLAIMER:** Please be aware that operating a DIY laser cutter can be dangerous and requires full awareness of the risks involved. You build the machine and you will have to make sure it is safe. The instructions of the Lasersaur project and related software come without any warranty or guarantees whatsoever. All information is provided as-is and without claims to mechanical or electrical fitness, safety, or usefulness. You are fully responsible for doing your own evaluations and making sure your system does not burn, blind, or electrocute people.

Some Notes about Using Eagle
=============================

Eagle is quite powerful but also awkward to use. It's easy to forget how to command the UI.

When designing the schematic
------------------------------
- import parts libraries, Library->Use
- some parts like the NAND gates require you to press the "Invoke" button and place power and ground. Don't ask me why.
- Once the schematic is done, run the electrical checks Tools->Erc

When laying out the board
--------------------------
- load design rules, Tools->Drc  (dru/LasaurShield.dru)
- place components, move/rotate to optimize the ratsnest
- color layers as needed, View->Display/hide layers
  - 121 _tsilk  ... is top silkscreen
  - 122 _bsilk  ... is bottom silkscreen
- run autoroute, 
  - The power of the autorouter is that it can be used incrementally. Some wires can be drawn manually and the autorouter can finish the rest. 
  - Another great approach is to draw some wires roughly (e.g. on one side of the board) then autoroute, rip the manual wires and autoroute again. This way the autorouter follows the general idea but draws the wires nicely.
- if the autorouter should use different trace widths this can be accomplished by defining net classes with different widths, Edit->Net classes
  - air wires of the ratsnest (it actually applies to the entire signal) can then be assigned to the various net classes

When creating the CAM Job (gerber files)
-----------------------------------------
- run final design rule check, Tools->Drc
- Open the CAM Processor, File->Cam Processor
- Open the CAM rule file, File->Open->Job   (cam/sparkfun-gerb274x.cam)
- Press "Process Job"
- At this point Eagle creates a bunch of files in the same directory as the board file. 
  - Top Copper (GTL)
  - Top Soldermask (GTS)
  - Top Silkscreen (GTO)
  - Bottom Copper (GBL)
  - Bottom Soldermask (GBS)
  - Bottom Silkscreen (GBO)
  - Drill File (TXT)
  - Drill Summary (dri)
- before sending these to a manufacturing house check them with [Viewplot](http://www.viewplot.com/) or by uploading a zip to [circuitpeople.com](http://circuitpeople.com/).




