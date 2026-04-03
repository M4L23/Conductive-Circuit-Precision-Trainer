# Conductive-Circuit-Precision-Trainer
A hardware-based precision game utilizing a closed-loop conductive circuit to provide real-time haptic and auditory feedback

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
