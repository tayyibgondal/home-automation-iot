# IoT-Driven Smart Home Automation System

## Problem Statement

In Pakistan, the residential sector accounts for approximately 46% of total electricity consumption, making it the nation’s largest energy consumer (NEPRA State of Industry Report, 2020). Over the past few years, the cost of electricity has soared by nearly 50%, rising from around PKR 14/kWh in 2017 to over PKR 20/kWh in 2023 (NEPRA, 2023). Meanwhile, inadequate fire safety leads to over 2,000 annual residential fire incidents in major cities, often due to the absence of functional smoke alarms (Pakistan Bureau of Statistics, 2019). These challenges highlight a pressing need for integrated solutions that enhance safety and curb escalating electricity costs. Homeowners require automated systems that offer reliable fire detection, smart energy control, and real-time analytics for informed decision-making.

## Project Description

Our proposed **IoT-Driven Smart Home Automation System** addresses these issues through a combination of sensors—primarily smoke, motion (PIR), light (LDR), temperature (TMP36), and gas detection (MQ-2 or similar)—and an Arduino UNO microcontroller, all linked to the ThingSpeak IoT platform for real-time data visualization. By continuously monitoring smoke levels, the system can trigger immediate alerts to mitigate fire risks. Concurrently, motion-based control of lighting and fans ensures that energy is consumed only when rooms are occupied, thereby reducing costs. A user-friendly dashboard provides homeowners with remote oversight and control, enabling data-driven optimizations and improvements to their home’s safety and efficiency.

## Application Requirements

- **Smoke Detection & Alerts**: Monitor smoke levels and send instant alarms or notifications once threshold levels are reached using the gas sensor (MQ-2).
- **Occupancy-Based Control**: Utilize PIR motion sensors to automate lighting and fan usage, preventing energy waste in unoccupied areas.
- **Real-Time Data Integration**: Send sensor readings to ThingSpeak for live monitoring and analysis, accessible via a web dashboard or mobile app.
- **Temperature Monitoring**: Measure room temperature using the TMP36 sensor, with data sent to ThingSpeak.
- **Scalability & Future Expansion**: Ensure a modular system design to accommodate additional sensors or upgrades as user requirements evolve.

## Email Alerts Integration

To enhance the responsiveness of the IoT-based home automation system, email alerts have been implemented as a key notification mechanism. The system leverages ThingSpeak's alert functionality to send real-time email notifications based on sensor thresholds. Below are some key features and examples:

### Distance Sensor Alerts
- **Purpose**: Alerts users when an object is detected at a critical distance.
- **Example**: "Entry Detected: Distance sensor reading is 16.00 cm, below the threshold of 50 cm."
- **Use Case**: Useful for monitoring unauthorized entry or proximity-based automation.

### Temperature Alerts
- **Purpose**: Warns users when the temperature exceeds a safe threshold.
- **Example**: "Warning: Temperature has reached 51.00°C. It's hot! Please check the environment."
- **Use Case**: Helps prevent overheating or fire hazards by triggering cooling systems or manual inspection.

### Gas Sensor Alerts
- **Purpose**: Notifies users about the presence of hazardous gas levels.
- **Example**: "Smoke Alert: Gas sensor reading is 298.00, exceeding the threshold of 200."
- **Use Case**: Ensures prompt action in case of fire or gas leaks, enhancing safety.

These alerts provide critical, real-time information to users, enabling immediate action to mitigate risks and optimize home automation systems.


<img width="176" alt="image" src="https://github.com/user-attachments/assets/7364bc54-057b-4ce4-93a5-5e2292e7d146" />
<img width="176" alt="image" src="https://github.com/user-attachments/assets/732e5ad4-0b52-4601-935d-ac5af5d72eb9" />
<img width="195" alt="image" src="https://github.com/user-attachments/assets/a2b0e3a2-0d60-47b6-8501-ddfcbd5e1179" />

## Summary of Visualizations

The system integrates various real-time and historical data visualizations for better monitoring and decision-making. These include:

1. **Temperature Graphs**:
   - Real-time temperature variations and average temperature trends to detect anomalies or changes in environmental conditions.

2. **Distance Sensor Graphs**:
   - Distance variation over time to track object movement or proximity.

3. **Lighting and Gas Sensor Graphs**:
   - Status of lighting systems and hazardous gas levels to monitor efficiency and safety.

4. **Histograms and Scatter Plots**:
   - Distribution and relationships between sensor readings, such as motion vs. lighting status.

Visualizations are accessible via the ThingSpeak dashboard, enabling users to interact with the data and extract actionable insights. 
 ![image](https://github.com/user-attachments/assets/2589d888-0e76-4119-b0ff-722a324a804b)
 ![image](https://github.com/user-attachments/assets/acca257c-8d94-4a2c-89a7-d1a925150e19)
 ![image](https://github.com/user-attachments/assets/9cb5f473-e284-4488-a09a-d5ec4b79d29a)
 ![image](https://github.com/user-attachments/assets/3f0743ed-e1e5-469e-8f9d-00857653d817)

## Setup Instructions

To replicate the IoT-Driven Smart Home Automation System, follow these setup steps:

### Prerequisites
1. **Hardware Requirements**:
   - Arduino UNO
   - Sensors:
     - PIR Motion Sensor
     - LDR Sensor
     - Gas Sensor (e.g., MQ-2)
     - Ultrasonic Sensor (HC-SR04)
     - Temperature Sensor (TMP36 or DHT11)
   - ESP8266 Wi-Fi Module
   - LCD Display (16x2)
   - Relay Module
   - Necessary wiring components (jumper wires, breadboard, resistors)

2. **Software Requirements**:
   - Arduino IDE (latest version)
   - ThingSpeak account (register at [ThingSpeak](https://thingspeak.com))
   - Required libraries:
     - `Adafruit DHT` for DHT11
     - `LiquidCrystal.h` for LCD control
     - ESP8266 Wi-Fi libraries for Arduino

---

### Step 1: Setting Up ThingSpeak
1. **Create a New Channel**:
   - Log in to ThingSpeak.
   - Create a channel with the following fields:
     - Field 1: Distance (cm)
     - Field 2: Light Level
     - Field 3: Gas Levels
     - Field 4: Motion Detection
     - Field 5: Temperature
   - Save the channel and note the **Channel ID**, **Write API Key**, and **Read API Key**.

2. **Configure Alerts**:
   - Navigate to ThingSpeak Alerts.
   - Set threshold values for sensors and define alert conditions.
   - Enter the email address(es) for notifications.

---

### Step 2: Arduino and ESP8266 Connections
1. **Connect the ESP8266**:
   - RX -> TX on Arduino (or SoftwareSerial pins)
   - TX -> RX on Arduino
   - VCC -> 3.3V
   - GND -> GND
2. **Connect Sensors**:
   - PIR Sensor:
     - OUT -> Arduino Digital Pin 8
   - Ultrasonic Sensor:
     - TRIG -> Arduino Digital Pin 7
     - ECHO -> Arduino Digital Pin 6
   - LDR:
     - Signal -> Arduino Analog Pin A0
   - Gas Sensor:
     - Signal -> Arduino Analog Pin A1
   - Temperature Sensor:
     - Signal -> Arduino Analog Pin A2
3. **Relay and LCD**:
   - Connect relay input to Digital Pin 13 for appliance control.
   - Wire the LCD to Arduino using appropriate digital pins (e.g., 12, 11, 5, 4, 3, 2).

---

### Step 3: Arduino Code Configuration
1. Open the Arduino IDE and load the project sketch.
2. Update the following variables:
   ```cpp
   String ssid = "Your_WiFi_SSID";
   String password = "Your_WiFi_Password";
   String apiKey = "Your_ThingSpeak_Write_API_Key";


