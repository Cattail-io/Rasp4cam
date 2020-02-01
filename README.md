# Rasp4cam
Multi Camera Adapter for Raspberry Pi
<img src="https://raw.githubusercontent.com/dodelal/Rasp4cam/master/photos/600x600/RPI_MultiCAM-4.jpg" width="250">
![image](https://raw.githubusercontent.com/dodelal/Rasp4cam/master/photos/600x600/pcbdesign.png) 

Simple camera multiplexer for Raspberry Pi allowed to connect up to 4 cameras to single CSI port. Only ONE camera can be enabled at a time. 

Reversed from [site](https://www.arducam.com/multi-camera-adapter-module-raspberry-pi/). 
Usage:
```
import RPi.GPIO as gp
import os

gp.setwarnings(False)
gp.setmode(gp.BOARD)

gp.setup(7, gp.OUT)
gp.setup(11, gp.OUT)
gp.setup(12, gp.OUT)

gp.setup(15, gp.OUT)
gp.setup(16, gp.OUT)
gp.setup(21, gp.OUT)
gp.setup(22, gp.OUT)

gp.output(11, True)
gp.output(12, True)
gp.output(15, True)
gp.output(16, True)
gp.output(21, True)
gp.output(22, True)

def main():
    gp.output(7, False)
    gp.output(11, False)
    gp.output(12, True)
    capture(1)

    gp.output(7, True)
    gp.output(11, False)
    gp.output(12, True)
    capture(2)

    gp.output(7, False)
    gp.output(11, True)
    gp.output(12, False)
    capture(3)

    gp.output(7, True)
    gp.output(11, True)
    gp.output(12, False)
    capture(4)

def capture(cam):
    cmd = "raspistill -o capture_%d.jpg" % cam
    os.system(cmd)

if __name__ == "__main__":
    main()

    gp.output(7, False)
    gp.output(11, False)
    gp.output(12, True)
```
