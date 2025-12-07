# Lab Module 10 - Edge Integration

Lab Module 10 implements bidirectional MQTT communication between the Constrained Device Application (CDA) and Gateway Device Application (GDA), enabling edge-based data processing, analytics, and actuator command triggering.

 Completed Exercises

PIOT-GDA-10-002: Message Listener Implementation

- Created three inner classes in `MqttClientConnector.java`:
  - `ActuatorResponseMessageListener` - Handles actuator command responses from CDA
  - `SensorDataMessageListener` - Processes incoming sensor data (humidity, temperature, pressure)
  - `SystemPerformanceDataMessageListener` - Handles system performance metrics
- Updated `connectComplete()` callback to subscribe to CDA topics:
  - `PIOT/ConstrainedDevice/ActuatorResponse`
  - `PIOT/ConstrainedDevice/SensorMsg`
  - `PIOT/ConstrainedDevice/SystemPerfMsg`
- Implemented JSON deserialization using `DataUtil`
- Routed messages to appropriate `IDataMessageListener` callback methods



Implementation Details:
- Added `handleUpstreamTransmission()` stub method for future cloud integration
- Implemented humidity threshold analysis in `DeviceDataManager`:
  - Monitors humidity sensor data for threshold crossings
  - Triggers humidifier ON command when humidity falls below 30%
  - Triggers humidifier OFF command when humidity exceeds 50%
  - Uses time-based analysis (300 second threshold)
- Integrated actuator command publishing to CDA via MQTT
- Configuration-driven threshold management from `PiotConfig.props`

Key Files Modified:
- `src/main/java/programmingtheiot/gda/app/DeviceDataManager.java`
- `config/PiotConfig.props`

Configuration Parameters:

[GatewayDevice]
enableMqttClient = True
handleHumidityChangeOnDevice = True
humidityMaxTimePastThreshold = 300
nominalHumiditySetting = 40.0
triggerHumidifierFloor = 30.0
triggerHumidifierCeiling = 50.0
```

PIOT-INT-10-003: Integration Testing
Status: Complete

Test Results:
- ✅ CDA successfully publishes sensor data to MQTT broker
- ✅ GDA successfully subscribes and receives sensor data
- ✅ JSON serialization/deserialization working correctly
- ✅ Message routing to appropriate handlers functioning
- ✅ Upstream transmission placeholder invoked
- ✅ End-to-end MQTT communication verified

Architecture

System Components

┌─────────────────────┐         MQTT Broker        ┌─────────────────────┐
│                     │      (Mosquitto:1883)       │                     │
│  Constrained Device │◄────────────────────────────►│  Gateway Device     │
│  Application (CDA)  │                             │  Application (GDA)  │
│                     │                             │                     │
│  Python             │                             │  Java               │
│  - Sensors          │   Publish Topics:           │  - MqttClient       │
│  - Actuators        │   - SensorMsg               │  - DeviceDataMgr    │
│  - MqttClient       │   - SystemPerfMsg           │  - Analytics        │
│  - Simulators       │   - ActuatorResponse        │                     │
│                     │                             │                     │
│                     │   Subscribe Topics:         │                     │
│                     │   - ActuatorCmd             │                     │
└─────────────────────┘                             └─────────────────────┘
```

Data Flow

1. CDA → GDA (Sensor Data)
   - CDA generates/reads sensor data
   - Serializes to JSON using `DataUtil`
   - Publishes to `PIOT/ConstrainedDevice/SensorMsg`
   - GDA receives via `SensorDataMessageListener`
   - DeviceDataManager analyzes data
   - Upstream transmission invoked

2. GDA → CDA (Actuator Commands):
   - GDA analyzes sensor data for threshold crossings
   - Creates `ActuatorData` command
   - Serializes to JSON
   - Publishes to `PIOT/ConstrainedDevice/ActuatorCmd`
   - CDA receives and executes command

Prerequisites

Software Requirements
- Java 11 or higher
- Python 3.9 or higher
- Eclipse IDE (with PyDev for Python)
- Mosquitto MQTT Broker
- Maven (for dependency management)

 Dependencies
- Eclipse Paho MQTT Client (Java)
- Eclipse Paho MQTT Client (Python)
- Californium CoAP Framework
- Sense HAT Emulator (optional)

Installation & Setup

 1. Clone Repository
bash
git clone https://github.com/empress-t-png/gda-java-components.git
cd gda-java-components
git checkout labmodule10

 2. Configure MQTT Broker
```bash
# Start Mosquitto
sudo systemctl start mosquitto
sudo systemctl enable mosquitto

# Verify it's running
sudo systemctl status mosquitto


3. Configure GDA
Edit `config/PiotConfig.props`:
```properties
[GatewayDevice]
enableMqttClient = True
enableSystemPerformance = True

[Mqtt.GatewayService]
host = localhost
port = 1883
enableAuth = False
enableCrypt = False

Running the Application

 Start GDA
1. Open Eclipse
2. Right-click `src/main/java/programmingtheiot/gda/app/GatewayDeviceApp.java`
3. Select **Run As → Java Application**

Expected Console Output:

INFO: Initializing GDA...
INFO: Starting GDA...
INFO: Connecting to MQTT broker: tcp://localhost:1883
INFO: Connected to broker: tcp://localhost:1883 (reconnect = false)
INFO: Subscribing to topic: PIOT/ConstrainedDevice/ActuatorResponse
INFO: Subscribing to topic: PIOT/ConstrainedDevice/SensorMsg
INFO: Subscribing to topic: PIOT/ConstrainedDevice/SystemPerfMsg
INFO: GDA started successfully.


 Testing

 Unit Tests
Run JUnit tests in Eclipse:
bash
src/test/java/programmingtheiot/part03/integration/connection/
├── MqttClientPerformanceTest.java
├── MqttClientConnectorTest.java
└── DeviceDataManagerWithCommsTest.java


Integration Tests
1. Start Mosquitto MQTT broker
2. Start GDA application
3. Start CDA application
4. Verify bidirectional communication in logs
5. Adjust sensor values to trigger threshold crossings
6. Verify actuator commands are sent

