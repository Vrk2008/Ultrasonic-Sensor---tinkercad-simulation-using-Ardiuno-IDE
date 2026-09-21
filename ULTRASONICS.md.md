ULTRASONIC SENSOR

📘 Project Description

This project focuses on designing and simulating an **automated distance tracking system** that provides real-time proximity feedback. Using high-frequency sound waves, the system calculates the absolute distance between the sensor and an incoming obstacle. It acts as a safety barrier by dynamically switching indicators (LEDs) based on user-defined safe zones and hazard thresholds, mimicking real-world industrial and automotive safety mechanisms.

---

⚙️ Component Inventory

* **Arduino Uno R3**: The central microcontroller brain that processes timing signals and executes logic.  
* **HC-SR04 Ultrasonic Transducer**: The sensor module responsible for sending out sonic pulses and listening for their echo.  
* **Red LED**: The visual hazard indicator that illuminates when an object passes the critical threshold.  
* **Green LED**: The visual safety indicator that glows when the clear zone is uncompromised.  
* **220-ohm Resistors (×2)**: Current-limiting resistors installed to protect the LEDs from overcurrent burnout.  
* **Breadboard & Jumper Wires**: The structural platform and physical lines used to establish electrical connections.

---

🛠️ Step-by-Step Procedure

1. **Workspace Setup**: Open Autodesk Tinkercad Circuits, create a fresh design, and pull an Arduino Uno and breadboard into the workspace.  
2. **Power Distribution**: Link the Arduino 5V and GND pins directly to the positive and negative distribution rails of the breadboard.  
3. **Sensor Integration**: Mount the HC-SR04 sensor onto the breadboard. Run the VCC pin to the 5V rail, the GND pin to the ground rail, the Trig pin to Arduino Digital Pin 9, and the Echo pin to Digital Pin 10.  
4. **Output Indicators**: Insert the Green and Red LEDs into the breadboard. Connect their short legs (cathodes) to the ground rail. Attach a 220-ohm resistor to each long leg (anode), then wire the Green LED resistor to Pin 4 and the Red LED resistor to Pin 5.  
5. **Code Upload**: Open the Tinkercad text code editor, replace any default code with the provided Arduino sketch, and click **Start Simulation**.  
6. **Testing**: Click on the virtual sensor to move the simulated target obstacle. Observe the changes in the serial monitor and the toggling of the LEDs.

---

🔄 System Working Principle

\[Trigger Pin (High for 10µs)\] ➔ emits 8-pulse Sonic Burst (40 kHz)  
                                         │  
                                         ▼  
                               \[Hits Target Obstacle\]  
                                         │  
                                         ▼  
\[Echo Pin (High for Travel Time)\] 🖎 Return Signal Detected  
                                         │  
                                         ▼  
                 \[Arduino Calculates: Time × 0.034 / 2\]  
                                         │  
                                         ▼  
                 \[Threshold Logic Controls Output Pins\]

1. **Triggering**: The Arduino drives the sensor's Trig pin HIGH for exactly 10 microseconds. This tells the sensor to emit an ultrasonic burst composed of 8 sonic pulses at 40 kHz.  
2. **Time Tracking**: The moment the burst leaves, the Echo pin shifts to a HIGH state. It stays HIGH until the reflected sound waves bounce back to the sensor. The pulseIn() function calculates this precise flight duration in microseconds.  
3. **Math Conversion**: Because sound travels through air at roughly 0.034 cm/μs, the system multiplies the travel time by 0.034. It then divides the result by 2 because the wave had to travel to the object and back.  
4. **Decision Logic**: The software compares this calculated distance against a 15 cm benchmark. If the target is closer than 15 cm, the Arduino instantly cuts power to the green pin and energizes the red pin.

---

📊 Expected Simulation Results

* **Safe Zone (\> 15 cm)**: The Green LED glows steadily. The Serial Monitor continuously prints out stable readings (e.g., Target Distance: 45 cm, Target Distance: 112 cm).  
* **Hazard Zone (≤ 15 cm)**: The Green LED shuts off and the Red LED turns on. The Serial Monitor outputs immediate warnings (e.g., Target Distance: 8 cm).  
* **Out of Range (\> 400 cm or \< 2 cm)**: The system outputs boundary limits or zero constants, indicating the object is outside the sensor's physical constraints.

---

🚀 Future Scope & Enhancements

* **Multi-Zone Feedback**: Integrating an active piezo buzzer to generate variable-frequency audio pings that beep faster as an object approaches, matching commercial parking systems.  
* **Environmental Self-Correction**: Adding a DHT11 temperature sensor to actively update the speed-of-sound constant used in the math calculation, keeping distance metrics accurate in freezing or hot climates.  
* **Autonomous Collision Avoidance**: Porting this structural layout into an H-bridge motor driver configuration to build an autonomous rover capable of mapping surroundings and steering clear of walls.
<img width="640" height="568" alt="ultrasonic" src="https://github.com/user-attachments/assets/6c925436-38ea-445b-a300-c0ff1b0ecbac" />
<img width="725" height="453" alt="tinkerultra" src="https://github.com/user-attachments/assets/bbac7a11-0143-4447-a677-27049bb7f8ab" />

