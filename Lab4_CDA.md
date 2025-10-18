# Constrained Device Application (Connected Devices)

 Lab Module 04


Description

What does your implementation do?

This implementation adds Sense HAT emulator support to the CDA, creating six emulator classes for sensors (humidity, pressure, temperature) and actuators (humidifier, HVAC, LED display). The emulators use the pisense library to read real sensor data and control the LED display. When the Sense HAT emulator is unavailable, the system automatically falls back to simulation mode, ensuring functionality across different environments.

How does your implementation work?

All emulator classes inherit from BaseSensorSimTask or BaseActuatorSimTask and initialize a SenseHAT instance based on the enableEmulator configuration flag. Sensor emulators override generateTelemetry() to read from Sense HAT sensors, while actuator emulators override _activateActuator() and _deactivateActuator() to display messages on the LED screen. SensorAdapterManager and ActuatorAdapterManager use dynamic module loading with import_module() to instantiate either simulators or emulators at runtime, providing seamless switching between modes without code changes.

 Code Repository and Branch

URL: https://github.com/empress-t-png/cda-python-components/tree/labmodule04
![Lab Module 04 UML Class Diagram](./lab04-class-diagram.png)

The UML diagram shows the class hierarchy with BaseSensorSimTask and BaseActuatorSimTask as parent classes, the six emulator classes that extend them, and the two manager classes (SensorAdapterManager and ActuatorAdapterManager) that orchestrate the emulator instances.

 Unit Tests Executed


*Lab Module 03 Unit Tests (Regression Testing):*

    test_HumiditySensorSimTask
    test_PressureSensorSimTask
    test_TemperatureSensorSimTask
    test_HumidifierActuatorSimTask
    test_HvacActuatorSimTask


*Lab Module 04 Unit Tests:*

    No new unit tests for Lab Module 04 (emulator functionality tested via integration tests)


 Integration Tests Executed


*Lab Module 03 Integration Tests (Regression Testing):*

    test_SensorAdapterManager
    test_ActuatorAdapterManager
    test_DeviceDataManagerNoComms
    test_ConstrainedDeviceApp


*Lab Module 04 Integration Tests:*

    test_HumidityEmulatorTask
    test_PressureEmulatorTask
    test_TemperatureEmulatorTask
    test_HumidifierEmulatorTask
    test_HvacEmulatorTask
    test_LedDisplayEmulatorTask
    test_SensorAdapterManager (with emulator support)
    test_ActuatorAdapterManager (with emulator support)
    test_ConstrainedDeviceApp (with emulator support)



