Microcontroller connections

each motor driver needs four pin connectons as follow

5v       5v output
EL       Motor enable input (5v)
Signal   speedometer output
Z/F      forward/reverse control (5v/GND)
VR       speed control (0..5v)
GND      ground

On the left side of ESP8266, we have
GPIO16 - EL
GPIO14 - Signal
GPIO12 - Forward/Reverse control
GPIO13 - Speed control

So, they will be for left motor

On the right side, we have
GPIO1 - EL
GPIO3 - Signal
GPIO5 - F/R control
GPIO4 - Speed control

and they will be for right motor
