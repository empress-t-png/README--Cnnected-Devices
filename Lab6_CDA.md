# Constrained Device Application (Connected Devices)
## Lab Module 06

Be sure to implement all the PIOT-CDA-* issues (requirements) listed at [PIOT-INF-06-001 - Lab Module 06](https://github.com/orgs/programming-the-iot/projects/1#column-10488434).

### Description

**What does your implementation do?**

This implementation adds MQTT (Message Queuing Telemetry Transport) publish/subscribe messaging capabilities to the Constrained Device Application (CDA). The MqttClientConnector class provides a robust interface for connecting to an MQTT broker (Mosquitto), publishing sensor data and system performance messages, subscribing to actuator command topics, and handling incoming messages through callback methods. The implementation integrates seamlessly with the DeviceDataManager to enable real-time communication between the CDA and other IoT components.

**How does your implementation work?**

The MqttClientConnector uses the Paho MQTT Python client library to establish connections with the MQTT broker running on localhost:1883. Upon initialization, it reads configuration parameters (host, port, keep-alive, QoS) from PiotConfig.props and sets up callback handlers for connection events, disconnection, message receipt, publish confirmation, and subscription confirmation. The class implements the IPubSubClient interface, providing publishMessage(), subscribeToTopic(), and unsubscribeFromTopic() methods. When DeviceDataManager starts, it automatically connects the MQTT client to the broker and subscribes to the CDA_ACTUATOR_CMD_RESOURCE topic to receive actuation commands. All MQTT operations are validated for proper resource names and QoS levels, with comprehensive logging to track message flow and connection status.

### Code Repository and Branch

URL: https://github.com/empress-t-png/cda-python-components/tree/labmodule06

### UML Design Diagram(s)

NOTE: The UML diagram will be added showing the MqttClientConnector class structure and its integration with DeviceDataManager.

[UML Diagram to be added]

### Unit Tests Executed

- ConfigUtilTest
- DataUtilTest
- SystemPerformanceDataTest
- SensorDataTest  
- ActuatorDataTest

### Integration Tests Executed

- MqttClientConnectorTest (all 8 tests passing):
  - testConnectAndDisconnect
  - testConnectAndCDAManagementStatusPubSub
  - testActuatorCmdPubSub
  - testNewActuatorCmdPubSub
  - testSensorMsgPub
  - testCDAManagementStatusPublish
  - testCDAManagementStatusSubscribe
  - testCDAActuatorCmdSubscribe
- SystemPerformanceManagerTest
- SensorAdapterManagerTest

