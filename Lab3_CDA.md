# Constrained Device Application (Connected Devices)

## Lab Module 03

### Description
My Lab Module 03 implementation creates a comprehensive data simulation and management infrastructure for the Constrained Device Application (CDA). the system stimulates three types of enviromental sensors,(temperature,humidity and pressure).

**What does your implementation do?**

My Lab Module 03 implementation creates a complete data simulation infrastructure for the Constrained Device Application (CDA). The system generates realistic sensor data for temperature, humidity, and pressure sensors, and simulates actuator responses through HVAC and humidifier components. The implementation includes a centralized DeviceDataManager that coordinates all data flow between sensors, actuators, and system performance monitoring. Additionally, the system implements automated control logic that triggers HVAC actuation when temperature readings exceed configured thresholds (18-20°C range). The implementation also includes comprehensive data container classes (SensorData, ActuatorData, SystemPerformanceData) that encapsulate all IoT telemetry and command data with proper getters/setters, supporting serialization and location awareness for multi-device deployments.

**How does your implementation work?**

The implementation follows an object-oriented design with clear separation of concerns. At the core is the SensorDataGenerator class, which produces realistic time-series data with configurable ranges and Gaussian randomization. Sensor simulation tasks (TemperatureSensorSimTask, HumiditySensorSimTask, PressureSensorSimTask) inherit from BaseSensorSimTask and use the generator to create realistic sensor readings. The SensorAdapterManager uses APScheduler to periodically poll sensor tasks every 5 seconds, collecting simulated data and passing it to the DeviceDataManager through callback methods. The DeviceDataManager analyzes incoming temperature data and, when values fall outside the 18-20°C threshold, creates ActuatorData commands that are sent to the ActuatorAdapterManager. The ActuatorAdapterManager processes these commands and triggers the appropriate actuator simulation tasks (HvacActuatorSimTask or HumidifierActuatorSimTask), which log actuation events with ON/OFF status and target values. The entire system is configuration-driven, with min/max values, thresholds, and polling rates defined in PiotConfig.props, and is coordinated by the ConstrainedDeviceApp entry point that initializes and starts all managers.

### Code Repository and Branch

URL: https://github.com/empress-t-png/cda-python-components/tree/labmodule03

### UML Design Diagram(s)

<img width="1008" height="905" alt="Lab03 uml diagram" src="https://github.com/user-attachments/assets/123c6b40-6ffe-4965-b2f7-a43e4c5884b5" />



..............................................................................................................................

### Unit Tests Executed

- test_ConfigUtil
- test_SensorDataGenerator
- test_ActuatorData
- test_SensorData
- test_SystemPerformanceData
- test_BaseIotData
- test_TemperatureSensorSimTask
- test_HumiditySensorSimTask
- test_PressureSensorSimTask
- test_HvacActuatorSimTask
- test_HumidifierActuatorSimTask

### Integration Tests Executed

- test_ConstrainedDeviceApp
- test_DeviceDataManager
- test_SensorAdapterManager
- test_ActuatorAdapterManager
- test_SystemPerformanceManager

