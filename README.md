# Myoelectric
Myoelectric arm code 
Introduction:	
My goal was to create a myoelectric prosthetic. I did this through 3D printing and a myo gesture band that picks up an EMG (Electromyogram, the electrical signal that control the muscle) signal from the wearer and sends it to an arduino which then talks to the servos so that it may recreate the gesture. 

Establishing the Bluetooth Connection:
I created a sync from the Myoband to the HM-11 Bluetooth chip with help from online forums where people attempted to achieve the same thing. This sync needed to be accomplished because there does not seem to be a way for the myo gesture band to talk to the arduino board without a computer in between directly so this bridged the gap. To get the bluetooth chip to connect to the myoband I had to upload custom firmware to the chip. To flash the chip a CC DeBugger is needed. One must be careful in soldering the Bluetooth chip so that none of the connections touch each other. The connections will be shown below. 

Figure 1. Bluetooth chip wires soldered to correct ports. Black-GND, Blue-Reset, Red-3.3V, Green-Target Voltage, Pink-RX, Orange-Debug Data, Yellow-Debug Clock. 

To attach to the debugger the connections between the HM-11 bluetooth chip and DeBugger need to be made correctly in order to successfully flash the code onto the chip. 

 
Figure 2. Shows the CC Debugger and numbers the ports with the reference point that faces the top of the Debugger. 

Using the large adapter that creates female ports for the bluetooth chip to connect into the Debugger. This will create something like the image below. 

**The adapter reverses the ports and so are relabeled above for convenience. 

Connections Bluetooth Chip to Debugger:
Now connect wires from HM-11 Bluetooth chip to the female ports of the CC Debugger adapter. Connections shown in table below. 
Black Wire 
Port 1 on adapter
Blue Wire
Port 7 on adapter
 Red Wire
Port 10 on adapter
Green Wire 
Port 2 on adapter
Orange Wire 
Port 4 on adapter
Yellow Wire
Port 3  on adapter
Pink Wire 
Port 9  on adapter

Connecting the Chip and Debugger to the computer:
Once connections are made between Bluetooth Chip and CC Debugger you can begin to flash the device. 
Plug in CC Debugger to the WINDOWS (This step must be down on a windows computer due to the flashing firmware does not work on a Mac) computer via the USB Cable that came with the Debugger.. 
-The light should be red. Press Reset on the top. If the chip is detected the light will turn green.
 *If light doe
s not turn green check and make sure all wires are in the correct place on the DeBugger Adapter and on the bluetooth chip make sure they are in the correct position and soldered well. 

Flashing the Firmware to the Bluetooth chip:
Download Myobridge firmware (link directly below) http://github.com/vroland/MyoBridge/blob/master/myobridgI’m e_firmware/Hex/MyoBridge_CC2541.hex
			-Right click “Raw”, Save as… 

Now to get flash  program ready to go follow the link  www.ti.com/tool/flash-programmer 
*Use version 1 

	Follow the SmartRF flash programmer and make sure the CC DeBugger is showing and highlighted in blue.
In the flash programmer click the “...” next to  the “flash image bar” within the smart setup add the Myobridge firmware that was just downloaded (this should be  .hex)

In the lower left under “actions” select “Erase, program and verify” 

Then click “perform actions” bar at the bottom - this starts the flashing of the chip

Wait until the bar is fully loaded and it says “Erase, program, and verify OK” 

*Once verified the bluetooth chip is ready to go as long as the CC Debugger light is green (if not double check the download)
**You may now unplug and set aside the DeBugger it will not be needed again but keep the Bluetooth Chip and do not remove any of its wires. 

Connecting Bluetooth Chip to Arduino Uno:
Wires from Chip 
Port on Arduino Uno 
Red Wire 
3.3V 
Black Wire 
GND(the one directly above Vin)
White Wire (via a voltage divider) 
Port 3 
Green Wire 
Port 2
*the rest of the wires on the bluetooth chip are not necessary now but it doesn’t hurt to keep them

Image of the connections are below and from https://github.com/vroland/MyoBridge/wiki/Getting-Started-with-MyoBridge-Library 



Testing the connection with the Myo Gesture Band
-Plug the Arduino Uno into the computer (Mac or Windows)
-Download the Arduino IDE 
		https://www.arduino.cc/en/Main/Software 

-Now you have to add the MyoBridge library to the Arduino for the code to work        		https://github.com/vroland/MyoBridge
                    		-Click clone or download
                    		-click download zip
-Go into zip folder
 -> Arduino 
->libraries
 
Here there will be a folder titled MyoBridge Create a new folder with only the contents of this folder inside and then convert it to a Zip file (right click and there should be an option to Compress or zip the folder, do this)
 
        	-Open the Arduino IDE
 -click on sketch in the top left
 -select “include libraries”
 -click ‘add zip library’ 
 -browse and insert the myobridge zip that was made.
