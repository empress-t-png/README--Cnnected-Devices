 Lab 12 – Gateway Device Application (GDA) & CSF Humidity Actuation

 Overview

This project implements cloud-triggered actuation for IoT devices through the Gateway Device Application (GDA) and Cloud Service Function (CSF) humidity actuation scripts. It satisfies the lab requirement:

Cloud can trigger actuator via LED commands and humidity-driven fan actuation.

Key Features

- Dual MQTT connections:
  -Local Broker:`localhost:1883` for device communication.
  - Cloud Service:Configured for Ubidots (or similar cloud service).
- Subscribes to actuator command topic:

Repository: https://github.com/empress-t-png/gda-java-components  
labmodule12


 - Commands are JSON-formatted:
- `{"value":1.0}` → LED ON
- `{"value":0.0}` → LED OFF
- CSF humidity actuation monitors humidity and triggers fan actuation:
- Topic: `actuation/humidity_fan`
- Fan ON/OFF threshold: 55% humidity
- Maintains last 30 readings for averaging



 Architecture

 GDA

- CloudClientConnector: Manages cloud connectivity and MQTT listeners.
- DefaultDataMessageListener:Receives actuator commands and forwards `ActuatorData`.
- *DeviceDataManager: Handles device-level processing of actuator data.


CSF Humidity Actuation

-csf_humidity_actuation.py: Publishes fan ON/OFF commands to MQTT based on humidity.
- humidity_actuation.py:Helper functions for actuation logic.
- *DeviceDataManager.py:Updated to handle new actuator data types.

---

 Repository

- Repository: [GDA Java Components](https://github.com/empress-t-png/gda-java-components)  
- Branch: `labmodule12`

---

Unit Tests

Executed tests include:

- `CloudClientConnectorTest`  
- `MqttClientConnectorTest`  
- `DeviceDataManagerTest`  
- `DataUtilTest` (extended for ActuatorData JSON parsing)  
- `ConfigUtilTest`  
- `ResourceNameEnumTest`  
- `ActuatorDataTest`  
- `SensorDataTest`  
- `SystemPerformanceManagerTest`  
- All previous tests from Lab Modules 01–11  

---

 Integration Tests

- `CloudActuationIntegrationTest` – Verifies end-to-end cloud command ON/OFF cycles  
- `MqttConnectivityTest` – Validates dual MQTT connections (local + cloud)  
- `DeviceDataManagerIntegrationTest` – Tests full actuator command flow  
- `SystemIntegrationTest` – Validates GDA startup and service connectivity  
- `JSONParsingTest` – Validates `{"value":1.0}` and `{"value":0.0}` formats  
- `ErrorHandlingTest` – Tests graceful handling of invalid JSON inputs  
- CSF humidity actuation tested with 1-hour simulated humidity data  

 Lab Module 12 - Data Visualization Screenshots

 Requirement #3: Data Collection and Visualization
The following screenshots show sensor and system performance data collected over 1+ hour with 200+ samples, visualized in Ubidots.

Temperature Sensor Data

 Humidity Sensor Data
![Humidity Data](Screenshot%20from%202025-12-14%2008-58-36.png)

 Pressure Sensor Data
![Pressure Data](Screenshot%20from%202025-12-14%2008-48-40.png)

Screenshots captured: December 14, 2025  
Total samples: 200+ per variable  
Collection period:1+ hour continuous testing

