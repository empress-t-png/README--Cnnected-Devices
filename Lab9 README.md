Constrained Device Application (Connected Devices)

 Lab Module 09

Be sure to implement all the PIOT-CDA-* issues (requirements) listed at [PIOT-CDA-09-005-A, PIOT-CDA-09-006, PIOT-CDA-09-100](https://github.com/orgs/programming-the-iot/projects/1).

Description

This implementation enhances the Constrained Device Application with complete CoAP client functionality by adding DELETE and OBSERVE operations to the existing CoAP client connectors. The implementation provides both synchronous and asynchronous CoAP client capabilities, enabling the CDA to interact with CoAP servers using all standard CoAP methods including GET, POST, PUT, DELETE, and OBSERVE for real-time resource monitoring.

The implementation works through two complementary CoAP client connectors: AsyncCoapClientConnector using the aiocoap library for asynchronous operations, and CoapClientConnector using CoAPthon3 for synchronous operations. The DELETE functionality allows the CDA to remove resources from CoAP servers with support for both CONFIRMABLE and NONCONFIRMABLE message types. The OBSERVE functionality enables the CDA to subscribe to resource updates and receive real-time notifications through callback handlers, which parse incoming ActuatorData messages and forward them to the DeviceDataManager for processing.

 Code Repository and Branch

URL: https://github.com/empress-t-png/cda-python-components/tree/default

 UML Design Diagram(s)


Unit Tests Executed

- test_CoapClientConnector (all methods including new OBSERVE functionality)
- test_CoapAsyncClientConnectorTest (DELETE functionality verification)
- test_CoapClientPerformance (performance baseline)
- ConfigUtilTest (configuration verification)
- DataUtilTest (JSON serialization/deserialization)
- ResourceNameEnumTest (resource path validation)

 Integration Tests Executed

- test_CoapClientConnector.py (full CoAP client integration)
- test_CoapServerAdapter.py (server-client interaction)
- test_MqttClientConnector.py (ensure no regression in MQTT functionality)
- test_CoapClientPerformance.py (performance validation)
- DeviceDataManagerTest (end-to-end data flow)
- test_async_coap_delete.py (async DELETE functionality)
- test_delete_simple.py (DELETE method verification)


