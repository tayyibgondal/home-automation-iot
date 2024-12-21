# IoT-Driven Smart Home Automation System

## 1. Problem Statement
In Pakistan, the residential sector accounts for approximately **46%** of total electricity consumption, making it the nation’s largest energy consumer (NEPRA State of Industry Report, 2020). Over the past few years, the cost of electricity has also **soared by nearly 50%**, rising from around **PKR 14/kWh in 2017 to over PKR 20/kWh in 2023 (NEPRA, 2023)**. Meanwhile, inadequate fire safety leads to **over 2,000** annual residential fire incidents in major cities, often due to the absence of functional smoke alarms (Pakistan Bureau of Statistics, 2019). These challenges highlight a pressing need for integrated solutions that enhance safety and curb escalating electricity costs. Homeowners require automated systems that offer reliable fire detection, smart energy control, and real-time analytics for informed decision-making.

## 2. Project Description
Our proposed **IoT-Driven Smart Home Automation System** addresses these issues through a combination of sensors—primarily smoke, motion (PIR), and light (LDR)—and an Arduino UNO microcontroller, all linked to the ThingSpeak IoT platform for real-time data visualization. By continuously monitoring smoke levels, the system can trigger immediate alerts to mitigate fire risks. Concurrently, motion-based control of lighting and fans ensures that energy is consumed only when rooms are occupied, thereby reducing costs. A user-friendly dashboard provides homeowners with remote oversight and control, enabling data-driven optimizations and improvements to their home’s safety and efficiency.

## 3. Application Requirements
1. **Smoke Detection & Alerts**  
   - Monitor smoke levels and send instant alarms or notifications once threshold levels are reached.
2. **Occupancy-Based Control**  
   - Utilize PIR motion sensors to automate lighting and fan usage, preventing energy waste in unoccupied areas.
3. **Real-Time Data Integration**  
   - Send sensor readings to ThingSpeak for live monitoring and analysis, accessible via a web dashboard or mobile app.
4. **Scalability & Future Expansion**  
   - Ensure a modular system design to accommodate additional sensors or upgrades as user requirements evolve.

---

# ThingSpeak Construction Documentation

## Introduction
This document provides an overview of how to set up and use ThingSpeak for our IoT-Driven Smart Home Automation System, which monitors smoke levels, detects motion, and manages lighting/fan control through an Arduino UNO. It explains how sensor data is transmitted to ThingSpeak for real-time monitoring, visualization, and analysis.

## Prerequisites
1. **ThingSpeak Account**  
   - Sign up at [ThingSpeak.com](https://thingspeak.com/) or log in using your MathWorks credentials.
2. **Arduino UNO** with necessary sensors:  
   - **PIR Sensor** (for motion detection)  
   - **LDR Sensor** (for ambient light detection)  
   - **Gas Sensor** (for smoke/gas level monitoring)
3. **ESP8266 or Compatible Wi-Fi Module** for internet connectivity.
4. **Installed Arduino IDE** (or an equivalent environment) on your computer.
5. **Libraries** (optional if required by your code):  
   - `LiquidCrystal.h` for LCD control  
   - Additional libraries for Wi-Fi configuration if needed

## Step-by-Step Setup

### 1. Create a New Channel
1. **Log in to ThingSpeak**: Go to your ThingSpeak dashboard and click **Channels**.
2. **Click “New Channel”**: Provide a name (e.g., _Smart Home Automation_) and a short description.
3. **Define Fields**: You can create up to 8 fields per channel. For this project, we use:
   - **Field 1**: Distance (cm) from the ultrasonic sensor
   - **Field 2**: Light Level (LDR sensor)
   - **Field 3**: Gas Sensor Value
   - **Field 4**: Motion Detection (PIR)
4. **Save Channel**: After saving, ThingSpeak will generate:
   - **Channel ID**  
   - **Write API Key**  
   - **Read API Key** (if you need to retrieve data)

### 2. Obtain API Key
1. **Go to “API Keys”**: In your channel’s settings, navigate to the **API Keys** tab.
2. **Copy the Write API Key**: This key is used in the Arduino code for sending sensor data to your ThingSpeak channel.

### 3. Configuring Arduino and ESP8266
1. **Connect ESP8266 to Arduino**:  
   - **RX -> TX** on Arduino (Pin 0 if using default serial, or use SoftwareSerial if you prefer)  
   - **TX -> RX** on Arduino  
   - **GND -> GND**  
   - **VCC -> 3.3V** (Ensure a stable 3.3V supply for the ESP8266)
2. **Update Code with Credentials**:  
   ```cpp
   // Replace these with your own details
   String ssid     = "Your_WiFi_SSID";
   String password = "Your_WiFi_Password";
   String apiKey   = "YOUR_THINGSPEAK_WRITE_API_KEY";

