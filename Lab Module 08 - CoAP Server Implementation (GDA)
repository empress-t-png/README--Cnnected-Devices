Lab Module 08 - CoAP Server Implementation (GDA)

This lab module implements a CoAP (Constrained Application Protocol) server in the Gateway Device Application (GDA) using Java and the Californium library. The server handles requests from CoAP clients and manages communication with the Constrained Device Application (CDA).
Implementation Approach
For Lab Module 08, I chose to implement the CoAP Server in the GDA rather than the CDA. According to the lab instructions, students can choose either:
Option A: CoAP Server in GDA + CoAP Client in CDA (Lab Module 09) 
Option B: CoAP Server in CDA + CoAP Client in GDA (Lab Module 09)

 Architecture
System Components

┌──────────────────────────┐
│   GatewayDeviceApp       │
│   (Main Application)     │
└──────────────────────────┘
           │
           ▼
┌──────────────────────────┐
│   DeviceDataManager      │
│   (Central Manager)      │
└──────────────────────────┘
           │
           ▼
┌──────────────────────────┐
│   CoapServerGateway      │
│   (CoAP Server)          │
│   Port: 5683             │
└──────────────────────────┘
           │
           ▼
┌──────────────────────────┐
│GenericCoapResourceHandler│
│   (9 instances)          │
│   - GET, POST            │
│   - PUT, DELETE          │
└──────────────────────────┘


 Components Implemented

1. CoapServerGateway
   - Main CoAP server implementation
   - Manages server lifecycle (start/stop)
   - Registers and manages CoAP resources
   - Uses Californium library on port 5683

2. GenericCoapResourceHandler
   - Handles CoAP requests (GET, POST, PUT, DELETE)
   - Provides resource-specific responses
   - Logs request handling for debugging

3.DeviceDataManager Integration
   - Initializes CoAP server on startup
   - Registers all 9 CDA resources
   - Manages server lifecycle

