Gateway Device Application (Connected Devices)
Lab Module 08

Be sure to implement all the PIOT-GDA-* issues (requirements) listed at [PIOT-INF-08-001 - Lab Module 08](https://github.com/orgs/programming-the-iot/projects/1).

Description

What does your implementation do?

My Lab Module 08 implementation creates a complete CoAP (Constrained Application Protocol) server within the Gateway Device Application (GDA) using the Eclipse Californium library. The server provides request/response communication capabilities for IoT devices, enabling the GDA to receive sensor data and system performance metrics from the Constrained Device Application (CDA), as well as send actuator commands back to the CDA. The implementation supports three primary resources: SystemPerfMsg for system performance data, SensorMsg for telemetry data, and ActuatorCmd for actuator commands. All resources are organized in a hierarchical structure following the pattern PIOT/ConstrainedDevice/ResourceName, providing a clean and organized API for IoT communication.

How does your implementation work?

The implementation begins with the CoapServerGateway class, which manages the Californium CoapServer instance and handles server lifecycle operations including initialization, starting, and stopping. During initialization, the server creates three specialized resource handlers: UpdateSystemPerformanceResourceHandler and UpdateTelemetryResourceHandler process incoming PUT requests containing JSON-formatted data from the CDA, converting them to Java objects using DataUtil and forwarding them to DeviceDataManager via callback methods. The GetActuatorCommandResourceHandler implements the CoAP OBSERVE pattern, allowing CDA clients to subscribe and receive automatic notifications when actuator commands are updated. All resource handlers are registered using a hierarchical chain registration system implemented in createAndAddResourceChain(), which parses resource names and builds a tree structure of CoapResource objects. The server integrates with DeviceDataManager through the IDataMessageListener and IActuatorDataListener interfaces, enabling seamless data flow between the CoAP protocol layer and the application's business logic.

Code Repository and Branch

URL: https://github.com/empress-t-png/gda-java-components/tree/labmodule08

 UML Design Diagram(s)

![Lab Module 08 UML Class Diagram](lab08-uml-class-diagram.png)


NOTE: The CoAP server architecture follows a layered design with CoapServerGateway as the facade, three specialized resource handlers extending CoapResource, and integration with DeviceDataManager through listener interfaces. The hierarchical resource structure (PIOT/ConstrainedDevice/ResourceName) is implemented using a composite pattern with CoapResource nodes.

Unit Tests Executed

- ConfigUtilTest
- SystemPerformanceDataTest
- ActuatorDataTest
- SensorDataTest

Integration Tests Executed

- GatewayDeviceAppTest (CoAP server initialization and startup)
- Manual testing: Started GDA and verified CoAP server on port 5683
- Manual testing: Verified resource handler chain registration for all three resources
- Manual testing: Confirmed hierarchical resource paths (PIOT/ConstrainedDevice/ActuatorCmd, PIOT/ConstrainedDevice/SensorMsg, PIOT/ConstrainedDevice/SystemPerfM

