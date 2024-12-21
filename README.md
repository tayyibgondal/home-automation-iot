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

## ThingSpeak Construction Documentation

### Introduction

This document provides an overview of how to set up and use ThingSpeak for our IoT-Driven Smart Home Automation System, which monitors smoke levels, detects motion, manages lighting/fan control, and tracks temperature through an Arduino UNO. It explains how sensor data is transmitted to ThingSpeak for real-time monitoring, visualization, and analysis.

### Prerequisites

- **ThingSpeak Account**: Sign up at ThingSpeak.com or log in using your MathWorks credentials.
- **Arduino UNO with necessary sensors**:
  - PIR Sensor (for motion detection)
  - LDR Sensor (for ambient light detection)
  - Gas Sensor (for smoke/gas level monitoring, e.g., MQ-2)
  - TMP36 Sensor (for temperature monitoring)
  - ESP8266 or Compatible Wi-Fi Module for internet connectivity.
- **Installed Arduino IDE** (or an equivalent environment) on your computer.
- **Libraries** (optional if required by your code):
  - `LiquidCrystal.h` for LCD control
  - Additional libraries for Wi-Fi configuration if needed.

### Step-by-Step Setup

1. **Create a New Channel**
   - Log in to ThingSpeak: Go to your ThingSpeak dashboard and click Channels.
   - Click “New Channel”: Provide a name (e.g., Smart Home Automation) and a short description.
   - Define Fields: Create up to 8 fields for this project:
     - **Field 1**: Distance (cm) from the ultrasonic sensor
     - **Field 2**: Light Level (LDR sensor)
     - **Field 3**: Gas Sensor Value (MQ-2 or similar)
     - **Field 4**: Motion Detection (PIR)
     - **Field 5**: Temperature (from TMP36)
   - Save Channel: ThingSpeak will generate:
     - Channel ID
     - Write API Key
     - Read API Key (for retrieving data)

2. **Obtain API Key**
   - Go to “API Keys”: In your channel’s settings, navigate to the API Keys tab.
   - Copy the Write API Key: This key is used in the Arduino code for sending sensor data to your ThingSpeak channel.

3. **Configuring Arduino and ESP8266**
   - **Connect ESP8266 to Arduino**:
     - RX -> TX on Arduino (Pin 0 if using default serial, or use SoftwareSerial if preferred)
     - TX -> RX on Arduino
     - GND -> GND
     - VCC -> 3.3V (Ensure a stable 3.3V supply for the ESP8266)

4. **Update Code with Credentials**
   Update the following in your Arduino sketch:

   ```cpp
   // Replace these with your own details
   String ssid     = "Your_WiFi_SSID";
   String password = "Your_WiFi_Password";
   String apiKey   = "YOUR_THINGSPEAK_WRITE_API_KEY";
