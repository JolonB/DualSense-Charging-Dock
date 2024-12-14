# DualSense Charging Dock

In the interest of increased repairability, I've compiled some useful information about the DualSense charging dock.

This includes schematics, pictures, and teardown instructions.

## Teardown

I found the following teardown guides very useful.
Rather than replicating instructions, I'll point you to these resources:

* [Video](https://www.youtube.com/watch?v=xvCFaVB1jn4)
* [Text](https://www.ifixit.com/Answers/View/690457/Dualsense+Charging+Station+Tear+Down+Guide)

Personally, I found the video guide to be more useful.

## Pictures

Images can be found in `assets/images`.

## Schematics

Schematics can be found in the `charging-dock` directory.
These were created using KiCad 8.

The part numbers may not be exact as some of them are based entirely off the two letters written on top.
In most cases, I was unable to get the values of resistors and capacitors, and it is difficult to work out what they should be without knowing the specifications of the other components.
The components with markings are described below:

* WP25141: Current-limited switch. Has enable input to allow power to pass from IN to OUT. Fault detection pin is not connected. I believe this is used for cutting power to the controllers, however, in my simulations, it only works in an undervoltage situation, so won't protect against high-voltage inputs.
* 1AM: [A 3-terminal device, very likely an NPN transistor](https://smd.yooneed.one/code3141.html#code31414d). This is used for enabling the WP25141 switches. When the BJT is open, the output is enabled.
* E2: [Some type of diode, likely a Zener](https://smd.yooneed.one/code4532.html#code4532). I think this is used to only allow the BJT to turn close when the voltage exceeds some threshold. This prevents power reaching the controller in an over-voltage condition.
* GD: [Some type of diode, likely a Zener](https://smd.yooneed.one/code4744.html#code4744). I believe this is used for ESD protection on the input, so it just handles large voltage spikes. I suspect it could be KDZ36B.

Datasheets for the mentioned components can be found in `assets/datasheets`.

The barrel jack footprint is also much bigger than it should be; I just used the closest footprint built in to KiCad.
The charging pin PCB is also not very accurate because I couldn't take it out to measure.
