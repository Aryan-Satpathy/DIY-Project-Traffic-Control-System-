# Arduio (ino) file
This is the arduino (ino) file.

I used Adafruit_MCP23017 library for this project.
Other than that I used the Traffic and Pedestrains library that I made.

Basically the "counting mechanism" is as follows :

	1. We maintain priority of various traffic poles and the pedestrians class.
	2. Priority is added according to the traffic demand in that lane, a fixed constant increment and presence of Emergency vehicles (Though we do not let any emergency vehicle wait)
	3. They have specific weights, like traffic demand is multiplied to a weight, same with the fixed constant increment and Emergency vehicles.
	4. At anytime there are two possiblities : Either any of the poles or the pedestrians light has green signal  OR  None of the poles are green(Pole got red signal just last frame)
	5. If none of the poles are green, we find the maximum priority and we give that pole (/pedestrian lights) green, we also figure out green time according to max priority / sum of all priorities
	6. If we any of the poles are green we do not do any further processing
	7. After this is done, we call update loops for all the lanes
	8. This is normal execution of program and when there is emergency vehicle, this procedure is not followed. The lane is given green signal immediately and all other signals are turned red

The reason behind making another class pedestrians, even though it works almost similar to TrafficPole class is because we can vary various important parameters as per requirement.

For instance we can keep a greater orange time for pedestrians as they need more warning time that vehicles to safely reach the other side before red signal is shown.
