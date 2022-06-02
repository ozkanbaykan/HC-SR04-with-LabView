# HC-SR04 with LabView
In this project, the HC-SR04 ultrasonic distance sensor will be used to solve the porpoising problem of Formula 1 teams in their cars.
## Problem:
In aerodynamics, the faster the car accelerates, the greater the downforce produced by the car. With the increase in the downforce, the distance between the car and the ground decreases and eventually the distance becomes zero. With the distance being zero, the air flow behind the car becomes zero. The fact that the air flow under the car is zero causes the downforce to reset momentarily. This downforce reset causes bouncing on the car. After the bounce, there will be air flow under the car again, so downforce occurs again, and this process becomes a cycle. 

![FMb1BW2WQAATTKl](https://user-images.githubusercontent.com/97105233/170497733-d3fef7d4-3e88-4260-93ab-c66f14102697.jpg)

This cycle is called **"Porpoising"**. Porpoising decreases speed at the straight lines of the cars and makes them more unbalanced and unstable. Also it exhausts drivers physically and prevents them from focusing. 

## Solution:
It was stated that the main cause of the porpoising problem was the cessation of airflow under the car. This problem can be solved with an active suspension. Active suspensions are suspensions with variable stiffness and angle. If the stiffness can be adjusted on the suspension with the help of a sensor, the car can be prevented from touching the ground and thus the air flow under the car can be prevented from disappearing. In this way, the problem of porpoising can be eliminated. The sensor to be used to solve this problem is the **HC-SR04** ultrasonic distance sensor, which will measure the distance between the car and the ground.

## Used Materials and Tools:
* HC-SR04
* Arduino Uno
* LabView
* LINX

## Step 1: Setting Up HC-SR04
The sensor has Vin, GND, Trigger and Echo pins. Vin is connected to Arduino's 5V input, GND ground input, Trigger input 9 and Echo input 10. Arduino is connected to the COM3 port of the computer. The following code was written to use the sensor and data flow was provided from the sensor through the COM3 port.

![arduino](https://user-images.githubusercontent.com/97105233/171728344-be8a9b39-58bd-46b9-8b5b-11cf34ad4a81.png)

```c++
const int trigPin = 9;
const int echoPin = 10;
long duration;
int distance;
void setup() {
  pinMode(trigPin, OUTPUT); 
  pinMode(echoPin, INPUT); 
  Serial.begin(9600); 
}
void loop() {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;
  Serial.print("Distance: ");
  Serial.println(distance);
}
```
## Step 2: Setting Up LINX
LINX is a toolbox that allows us to use development boards such as arduino with labview. This toolbox must be installed in our system in order to view the data we receive from the sensor via labview. This toolbox is installed on the system via the NI Package Manager. 

## Step 3: VI Design
Three different ranges were determined for the condition of the suspensions. In cases where the distance between the car and the ground is less than 10 cm, the suspension will be stiffened, when it is between 10 and 20 cm, the suspension will work normally, and when it exceeds 20 cm, the suspension will be loosened. Decision mechanisms were established for these three different situations and leds were created for these situations on the front panel. Through the LINX toolbox we have installed, the sensor data we received from the arduino was transferred to the labview and the front panel, which will change according to this distance data, was created.

<img src="https://user-images.githubusercontent.com/97105233/171728496-bd2baf78-6a6c-4229-902c-ee940b32cf48.png" width="90%"></img> <img src="https://user-images.githubusercontent.com/97105233/171728545-41be8e6c-5501-4925-979d-c7bc079244c9.png" width="90%"></img> 

