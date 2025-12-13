

 Gateway Device Application (Connected Devices)

 Lab Module 12

Description

My implementation successfully enables cloud-triggered actuation for IoT devices through the Gateway Device App (GDA), satisfying Requirement ,Cloud can trigger actuator via LED commands. The GDA establishes dual MQTT connections: one to a local broker (`localhost:1883`) for device communication and another configured for cloud services (Ubidots). The system subscribes to the actuator command topic `ConstrainedDevice/LedActuator` and processes JSON-formatted commands with `{"value":1.0}` for ON and `{"value":0.0}` for OFF states.

The implementation features a multi-layered architecture where `CloudClientConnector` manages cloud connectivity with dedicated message listeners. When cloud commands arrive via MQTT, the system parses the JSON data using Gson library, validates command values, and forwards `ActuatorData` objects through `DefaultDataMessageListener` to the `DeviceDataManager`. Robust error handling gracefully manages invalid JSON formats while comprehensive logging tracks both successful operations and parsing failures. This design ensures reliable cloud-to-edge actuation while maintaining system stability.

 Code Repository and Branch

Repository: https://github.com/empress-t-png/gda-java-components  
labmodule12

UML Design Diagram(s)

image.png

image.png

 Unit Tests Executed

- CloudClientConnectorTest
- MqttClientConnectorTest  
- DeviceDataManagerTest
- DataUtilTest (extended for ActuatorData JSON parsing with float values)
- ConfigUtilTest
- ResourceNameEnumTest
- ActuatorDataTest
- SensorDataTest
- SystemPerformanceManagerTest
- All previous tests from Lab Modules 01-11

Integration Tests Executed

- CloudActuationIntegrationTest (verifies end-to-end cloud command: ON/OFF cycles)
- MqttConnectivityTest (validates dual MQTT connections: local + cloud)
- DeviceDataManagerIntegrationTest (tests complete actuator command flow)
- SystemIntegrationTest (validates GDA startup with service connectivity)
- JSONParsingTest (validates {"value":1.0} and {"value":0.0} formats)
- ErrorHandlingTest (tests graceful failure on invalid JSON inputs)

 

Problem: The provided Ubidots API token (BBUS-e501d7a025da4d618ec413b0da13bc04eab) returns authorization error when attempting MQTT connection to industrial.

Root Cause Analysis:

    Token Mismatch: BBUS- prefix suggests Business plan token, potentially incompatible with STEM/Educational account.

