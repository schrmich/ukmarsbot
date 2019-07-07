# Speed Performance

A robot meant for a contest should be designed for good performance. Mostly, this means the best top sped and acceleration. Turning performance is important as well but for now, consider only straight-line motion.

Getting the best performance is about choosing the right motor, gear ratio and wheel size while keeping the weight as low as possible.  All the micrometal gearmotors weight about the same so that alone will not influence the motor choice.

## Motors

There are many different types of motor in the rnage offered by sellers like Pololu and Pimoroni. They differ in the rated voltage and the motor power. All the Pimoroni motors are the same but Pololu offer High Power (HP), Medium Power (MP), and Low Power (LP) versions as well as a High Power version with carbon brushes (HPCB).

Practicaly, the choices are probably limited to just three motors. The others either take too much current from the battery or do not have enough power for good performance. That does not mean these are the only choice - that is up to the individual builder. These will make a good starting point though.

**Pimoroni 6 Volt** These are significantly cheaper than the Pololu motors and have a stall current of around 0.8 Amp making them suitable for pretty much any of the common motor drivers.

**Pololu 6 Volt MP** This motor has a little less power than the Pimoroni motor and a slightly lower stall current. They are pretty much the same as the Pimoroni motor otherwise except for being more expensive.

**Pololu 6 Volt HPCB** Also available withoutthe carbon brushes, these are significantly more powerful and run about 50% faster. The increased performance comes at the cost of a much higher stall current of around 1.5 Amps meaning that they may not be suitable for smaller motor drivers.

## Gearboxes

These motors all come with gerboxes. The purpose of gears is to slow the motor speed ahile increasing the torque (the turning force). For a better top speed, small gear ratios are best but, if the robot is heavy, acceleration will be poor. For better acceleration, high gear ratios are best but then the top speed will be limited. the most suitable gear ratios for these little motors in this application are likely to be in the range 5:1 to 30:1. Note that Pimoroni and Pololu gear motors offer slightly different ratios.

Here is a table showing, for each motor and gearbox, the theoretical maximum speed (in mm/s) that might be expected if the motor is driven with a 6 Volt supply. A real robot would be unlikely to reach this speed due to inefficiencies in the design or the motor drive. These are listed in order of gear ratio to match the table below where the encoder resolution is shown.


|Motor              | 25mm| 32mm|  60mm|  70mm|
|:------------------|----:|----:|-----:|-----:|
|Pololu 6V MP  5:1  | 5760| 7372| 13823| 16127|
|Pololu 6V MP  10:1 | 2880| 3686|  6912|  8063|
|Pololu 6V HPCB 10:1|	3927|	5027|	 9425| 10996|
|Pimoroni 6V 11:1   | 2356| 3016|  5655|  6597|
|Pimoroni 6V 20:1   |	1374|	1759|	 3299|	3848|
|Pololu 6V HPCB 30:1|	1440|	1843|	 3456|	4032|

Before deciding that the fastest option is the best, have a look at ho the choice affects the encoder resolution:

## Encoder Resolution

For good controllability, the robot needs to have the highest possible encoder resolution. That is, travelling 1 meter on the ground should generate the highst possible number of encoder counts.

For the micrometal gearmotors that are common, the best option for ready-made encoders is probably the magnetic ecoder set available from Pololu. These henerate two non-overlapping pulse trains allowing 6 edges per motor revolution to be counted. Se the [encoders document](encoder-software.md) for more details.

The motors have gear boxes that effectively multiply the count per wheel revolution. A 10:1 gearbox will give 10 x 6 = 60 counts per wheel revolution.

Bigger wheels cover a greater distance in one revolution so the distance represented by each count is also bigger. For a wheel with diapeter 32mm, the circumference is 32 * pi  = 100.5mm and so each count with a 10:1 gearbox represents 100.5/60 = 1.676mm.

For forward motion, the controller can add together the counts from the left and right motor to get a count for the speed and distance travelled. That effectively doubles the resolution so that the 10:1 gearbox plus 32mm wheels have an effective resolution of 0.838mm per count or 1194 counts per meter.

Here is a table showing the best effective resolution (in mm per count) for various gearbox ratios and wheel sizes. This assumes the counts are added together for left and right wheels.

|Ratio  |25mm |32mm |60mm |70mm |
|------:|:---:|:---:|:---:|:---:|
|    5:1|1.309|1.676|3.142|3.665|
|   10:1|0.654|0.838|1.571|1.833|
|   11:1|0.595|0.762|1.428|1.666|
|   20:1|0.327|0.419|0.785|0.916|
|   30:1|0.218|0.279|0.524|0.611|

## Summary

There are plenty of choices for the motor and wheel combination used to drive the robot. the choice may be for finest encoder resolution, maximum speed, best acceleration or some com[promise of all these. The combination that is best for one contest may not suit another. Finding the best all round setup is a decision left to the builder.
