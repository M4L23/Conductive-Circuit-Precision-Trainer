# Conductive-Circuit-Precision-Trainer
A hardware-based precision game utilizing a closed-loop conductive circuit to provide real-time haptic and auditory feedback

![operationgif](https://github.com/user-attachments/assets/b3af5957-b740-4bfd-b342-a7272c4054d5)


Overview
This project is a classic "Operation" style game built to demonstrate basic circuit completion logic. The system uses a set of tweezers as a probe and a copper-lined "track." When the probe touches the track, the circuit completes, triggering a microcontroller to activate an auditory alarm (buzzer).

Technical Components
Microcontroller: ELEGOO UNO R3

Input: Conductive tweezers (Ground)

Target: Copper wire/tape (Digital Pin with Internal Pull-up)

Output: 5V Active Piezo Buzzer

Code Base: C++/Arduino

How it Works
The logic operates on a Normally Open (NO) circuit principle:

The digital pin is set to INPUT_PULLUP, keeping the signal HIGH by default.

The tweezers are tied to GND.

Upon collision, the tweezers ground the digital pin, pulling the signal LOW.

The software detects this state change and triggers the Buzzer output pin.

The Build
![image0 (1)](https://github.com/user-attachments/assets/c3c2c120-b414-4e75-8279-50534c2ccfab)
![image1 (1)](https://github.com/user-attachments/assets/c7efd991-80a4-4dce-a4b4-34a4e0b2fbd0)

Lessons Learned
Debouncing: I learned that physical contact can be "noisy," sometimes causing the buzzer to stutter. I implemented a small software delay (debounce) to ensure a clean, consistent sound.

Conductivity: Testing different metals for the "track" to ensure the lowest resistance for an immediate trigger.

Circuit

<img width="788" height="630" alt="image" src="https://github.com/user-attachments/assets/f9e09a1a-33c6-4573-8646-ded83f460217" />


Code

```cpp

const int touchPin = 2;
const int buzzerPin = 13;

void setup(){
  Serial.begin(9600);
  pinMode(touchPin, INPUT_PULLUP);
  pinMode(buzzerPin, OUTPUT);
}

void loop(){
  int state = digitalRead(touchPin);

  if (state == LOW){
      delay(50);
      digitalWrite(buzzerPin, HIGH);
  }else{
    digitalWrite(buzzerPin, LOW);
  }
}

```
