# 2 Hub Host Integration and Dual Connectivity Modes


#### 1 Standard Mode Integration (Hub as standard device to host)

      - USB HID Device Mode (Keyboard, mouse, generic HID)
      - USB MIDI Device Mode (Standard MIDI controller)
      - USB Audio Device Mode (Audio interface, control surface)
      - Bluetooth HID/MIDI Mode (Wireless standard devices)

#### 2 Drimit Link Mode Integration (Drimit Link software required on host)

      - Enhanced Protocol Communication
      - Full Grid State Synchronization
      - Advanced Feature Access (Telemetry, debug, OTA)
      - Multi-Platform Host Software Integration

#### 3 Cloud-Direct Mode Integration (Hub connects directly to cloud)

      - Cloud Protocol Stack Implementation
        - HTTPS REST API Integration (Configuration, authentication, management)
        - WebSocket Secure (WSS) Real-Time Communication (Control events, state sync)
        - Server-Sent Events (SSE) for Unidirectional Streaming (Telemetry, notifications)
        - Protocol Selection Logic and Fallback Mechanisms
      - Hub-to-Cloud Authentication and Security
        - Device Certificate-Based Authentication (mTLS)
        - API Key Management and Rotation
        - End-to-End Encryption for Control Messages
      - Cloud State Synchronization and Management
        - RESTful State Management (GET/PUT/PATCH operations)
        - WebSocket Event Streaming (Real-time grid state updates)
        - Conflict Resolution and State Merging Algorithms
      - Offline Operation and Cloud Reconnection Handling
        - Local State Caching and Persistence
        - Reconnection Strategy and Backoff Algorithms
        - Delta Synchronization on Reconnect

#### 4 Wireless Protocol Integration (Wi-Fi, Bluetooth, Ethernet)


#### 5 Cloud Services Integration and APIs

