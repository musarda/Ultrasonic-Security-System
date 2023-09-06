# Ultrasonic Security System

It is a **simple** tutorial on how to create **little a security** device using an **Arduino**.

> [!WARNING]  
> This is for Educational and Informational Purposes Only.

## Contents
- **[Setup](#setup)**
   * **[On Ultrasonic Sensor](#on-ultrasonic-sensor)**
   * **[LEDs](#leds)**
   * **[Example](#example)**
- **[Assembly - Breadboard](#assembly---breadboard)**
- **[Assembly - Ultrasonic Sensor](#assembly---ultrasonic-sensor)**
- **[Assembly - LEDs](#assembly---leds)**
- **[Assembly - Buzzer](#assembly---buzzer)**
- **[Code](#code)**
- **[Folders](#folders)**
- **[Clone](#clone)**
- **[License](#license)**

## Components

* **Arduino UNO**
* **Breadboard**
* **Buzzer**
* **Ultrasonic Sensor - HC-SR04**
* **Resistor 221 ohm**
* **LED**
* **Jumper wires**

## Project description

### Setup

<img src="https://github.com/musarda/Ultrasonic-Security-System/blob/main/src/img/img-1.png?raw=true" title="Setup" alt="Setup" width="400">

**Connect** a **red** wire from the **5V pin** on the **Arduino** to the **positive channel** of the **breadboard**. Connect a **black** wire from the **GND pin** on the **Arduino** to the **negative channel** of the breadboard:

```ino
Buzzer = pin 7
```
#### On Ultrasonic Sensor: 

```ino
Echo = pin 3 
Trig = pin 2 
```

#### LEDs: 

```ino
RedLED = pin 4 
YellowLED = pin 5 
GreenLED = pin 6 
```

#### Example

```ino
#define trigPin 2
#define echoPin 3
#define soundbuzzer 7
#define LEDlampRed 4
#define LEDlampYellow 5
#define LEDlampGreen 6 
```

The **green** wires connected to the **LEDs** should be connected in line to the **positive** side of the **LED**, while the **negative** side of the **LED** should be **connected** to the **negative channel** of the **breadboard** using a **220 ohm** resistor. 

> [!IMPORTANT]  
> Make Sure The Connections Are Made Correctly Otherwise It May Not Work Correctly.

### Assembly - Breadboard

<img src="https://github.com/musarda/Ultrasonic-Security-System/blob/main/src/img/img-breadboard.png?raw=true" title="img-breadboard" alt="img-breadboard" width="400">

Firstly, let's connect the **5V** and **GND pin** on the **Arduino** to the **breadboard**. As I mentioned before, be sure that the wire attached to the **5V pin** is connected to the **positive channel** of the **breadboard**, and the wire attached to the **GND pin** is connected to the **negative channel** of the **breadboard**.

### Assembly - Ultrasonic Sensor

<img src="https://github.com/musarda/Ultrasonic-Security-System/blob/main/src/img/img-hc-sr04.png?raw=true" title="img-hc-sr04" alt="img-hc-sr04" width="400">

Time to connect the **HC-SRO4 ultrasonic sensor**! A great tip is to place the ultrasonic sensor as far right to the **breadboard** as possible and make sure that it is facing out. Referring back to the **setup picture**, you should connect the **GND pin** on the **ultrasonic sensor** to the **negative channel** on the **breadboard**. Next connect the **Trig pin** on the sensor to pin **2** on the **Arduino** and connect the **Echo pin** on the sensor to pin **3** on the **Arduino**. Lastly, connect the **VCC pin** on the **ultrasonic sensor** to the **positive channel** on the **breadboard**. Refer to the picture above if anything gets confusing.

### Assembly - LEDs

<img src="https://github.com/musarda/Ultrasonic-Security-System/blob/main/src/img/img-led.png?raw=true" title="img-led" alt="img-led" width="400">

The next step is to connect the **LED's** to the **breadboard** and **Arduino**. If you need to, I highly recommend that you refer back to the setup picture **(Step 2)**, attaching the **LEDs** is pretty easy, there's a lot of repetition. Let's first attach the **Green LED**. So the way to do this, is to connect the anode **(the longer leg)** to pin **6** on the **Arduino** with a **green** wire, and to **connect** the cathode **(the shorter leg)** to the **negative channel** on the **breadboard**, using a **220 ohm** resistor. Then repeat that step for the **Yellow** and then the **Red LED**, make sure to **connect** the anode **(the longer leg)** of the **yellow LED** to pin **5** on the **Arduino** and then **connect** the anode of the **red LED** to pin **6**. Once you have done that, your setup should look similar to the picture above. 
**Resistors** are not absolutely necessary, however they are highly recommended to be used. 

### Assembly - Buzzer

<img src="https://github.com/musarda/Ultrasonic-Security-System/blob/main/src/img/img-1.png?raw=true" title="buzzer" alt="buzzer" width="400">

The last part of the setup for this, is connecting the **buzzer** to the **breadboard** and the **Arduino**. This is one of the easiest parts of the whole setup. All that is required to do is to connect the **longer leg** of the **buzzer** to pin **7** of the **Arduino** using a **green** wire and then connect the **shorter leg** of the **buzzer** to the **negative channel** of the **breadboard** using a **220 ohm** resistor. 
It is hıghly recommended to use a **resistor** in connecting the **shorter leg** of the **buzzer** to the **negative channel** of the **breadboard**. This greatly reduces the volume of the **buzzer** and prevent it from dying to quickly. 

## Code

- Pin Definitions:
  * `trigPin` is defined as the trigger pin of the ultrasonic sensor.
  * `echoPin` is defined as the echo pin of the sensor.
  * `soundbuzzer` is defined as a pin used for an audible alert through a buzzer.
  * `LEDlampRed` controls a red LED light.
  * `LEDlampYellow` controls a yellow LED light.
  * `LEDlampGreen` controls a green LED light.

- `sound` Variable:
  * The `sound` variable represents the frequency at which the buzzer will sound.

- `setup()` Function:
  * It initializes serial communication `(9600 baud)`.
  * Sets the pin modes: `trigPin` is set as an output, while `echoPin`, `LEDlampRed`, `LEDlampYellow`, `LEDlampGreen`, and `soundbuzzer` are set as input/output pins.
  * 
<details>
<summary>Code</summary>

```ino
void setup() {

    Serial.begin (9600);
    pinMode(trigPin,  OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(LEDlampRed, OUTPUT);
    pinMode(LEDlampYellow,  OUTPUT);
    pinMode(LEDlampGreen, OUTPUT);
    pinMode(soundbuzzer, OUTPUT);
}
```
</details>

- `loop()` Function:
  * It performs distance measurement with the **ultrasonic sensor**.
  * Then, it carries out different actions based on specific distance thresholds:
    - If the measured distance is less than **50 cm**, it turns on the **green LED**.
    - If the measured distance is less than **20 cm**, it turns on the **yellow LED**.
    - If the measured distance is less than **5 cm**, it turns on the **red LED** and activates the **buzzer** at a specific frequency.
    - If the measured distance is above **5 cm** or there is no valid distance measurement, it prints "Outside the permissible range of distances" to the serial monitor and turns off the buzzer.
    - It also prints the measured distance to the serial monitor.

<details>
<summary>Code</summary>

```ino
void  loop() {

    long durationindigit, distanceincm;
    
    digitalWrite(trigPin, LOW);  
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);

    durationindigit = pulseIn(echoPin, HIGH);
    distanceincm = (durationindigit/5) / 29.1;
 
    if (distanceincm < 50) {
        digitalWrite(LEDlampGreen, HIGH);
    }
    else {
        digitalWrite(LEDlampGreen,  LOW);
    }
  
    if (distance < 20) {
        digitalWrite(LEDlampYellow,  HIGH);
    }
    else {
        digitalWrite(LEDlampYellow,LOW);
    }

    if (distance  < 5) {
        digitalWrite(LEDlampRed, HIGH);
        sound = 1000;
    }
    else  {
        digitalWrite(LEDlampRed,LOW);
    }
 
    if (distanceincm > 5 ||  distanceinsm <= 0){
        Serial.println("Outside the permissible range of distances");
        noTone(soundbuzzer);
    }
    else {
        Serial.print(distance);
        Serial.println("  cm");
        tone(buzzer, sound);
    }
  
    delay(300);
  }
```
</details>

- It creates a loop with **delay(300)**, so the sensor periodically measures distance and processes the results.

<br>
<details>
<summary>Click To See All Code</summary>
 
**[Code](https://github.com/musarda/Ultrasonic-Security-System/tree/main/src/code)**

```ino
#define trigPin 2
#define echoPin 3
#define soundbuzzer 7
#define LEDlampRed 4
#define LEDlampYellow 5
#define LEDlampGreen 6 

int sound  = 500;


void setup() {

    Serial.begin (9600);
    pinMode(trigPin,  OUTPUT);
    pinMode(echoPin, INPUT);
    pinMode(LEDlampRed, OUTPUT);
    pinMode(LEDlampYellow,  OUTPUT);
    pinMode(LEDlampGreen, OUTPUT);
    pinMode(soundbuzzer, OUTPUT);
}

void  loop() {

    long durationindigit, distanceincm;
    
    digitalWrite(trigPin, LOW);  
    delayMicroseconds(2);
    digitalWrite(trigPin, HIGH);
    delayMicroseconds(10);
    digitalWrite(trigPin, LOW);

    durationindigit = pulseIn(echoPin, HIGH);
    distanceincm = (durationindigit/5) / 29.1;
 
    if (distanceincm < 50) {
        digitalWrite(LEDlampGreen, HIGH);
    }
    else {
        digitalWrite(LEDlampGreen,  LOW);
    }
  
    if (distance < 20) {
        digitalWrite(LEDlampYellow,  HIGH);
    }
    else {
        digitalWrite(LEDlampYellow,LOW);
    }

    if (distance  < 5) {
        digitalWrite(LEDlampRed, HIGH);
        sound = 1000;
    }
    else  {
        digitalWrite(LEDlampRed,LOW);
    }
 
    if (distanceincm > 5 ||  distanceinsm <= 0){
        Serial.println("Outside the permissible range of distances");
        noTone(soundbuzzer);
    }
    else {
        Serial.print(distance);
        Serial.println("  cm");
        tone(buzzer, sound);
    }
  
    delay(300);
}
```
</details>

### Folders

**[You can view the files here](https://github.com/musarda/Ultrasonic-Security-System/tree/main/src)**

## Clone

```git
git clone musarda/Ultrasonic-Security-System
```
## License
This project is **licensed** under the **[MIT License.](https://github.com/musarda/Ultrasonic-Security-System/blob/main/LICENSE)**
