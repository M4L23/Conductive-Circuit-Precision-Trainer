# Conductive-Circuit-Precision-Trainer
A hardware-based precision game utilizing a closed-loop conductive circuit to provide real-time haptic and auditory feedback

![operationgif](https://github.com/user-attachments/assets/b3af5957-b740-4bfd-b342-a7272c4054d5)


📝 Overview
This project is a modern take on the classic "Operation" style game, designed to demonstrate fundamental circuit completion and microcontroller logic. The system utilizes a pair of conductive tweezers as a probe and a custom copper-lined "track."

When the user’s hand slips and the probe contacts the track, the circuit completes, triggering a high-frequency auditory alarm via an active piezo buzzer.

🛠️ Technical Components
Microcontroller: ELEGOO UNO R3

Input Hardware: Conductive tweezers (tied to Ground)

Target Interface: Copper wire/tape (configured via Digital Pin with Internal Pull-up)

Output Hardware: 5V Active Piezo Buzzer

Language/Environment: C++ / Arduino IDE

⚙️ How it Works
The system operates on a Normally Open (NO) circuit principle:

Pull-up Logic: The digital input pin is set to INPUT_PULLUP, which uses the Arduino's internal resistor to hold the signal HIGH (5V) by default.

Grounding: The tweezers are connected directly to the common GND rail.

State Change: Upon collision, the tweezers ground the digital pin, pulling the signal LOW (0V).

Execution: The software detects this transition and immediately writes a HIGH signal to the buzzer output.

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

Lessons Learned
Signal Debouncing: During initial testing, physical contact was "noisy," causing the buzzer to oscillate. I implemented a software-based delay to ensure a clean, consistent auditory trigger.

Materials Science: I experimented with various conductive materials for the track, ultimately choosing copper for its low electrical resistance and immediate responsiveness.
