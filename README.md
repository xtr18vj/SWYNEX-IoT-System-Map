# SWYNEX-IoT-System-Map
## IoT Room Temperature Monitoring System

**Task:** IoT System Map  
**Type:** Conceptual design; no physical hardware required

### 1. Objective
Design a simple IoT system that monitors room temperature and humidity, sends measurements to a cloud service, and presents the data on a dashboard.

### 2. System components
| Layer | Component | Purpose |
|---|---|---|
| Sensing | DHT22 temperature/humidity sensor | Measures room temperature and relative humidity |
| Edge/controller | ESP32 | Reads sensor data, adds a timestamp, and prepares a data payload |
| Connectivity | Wi-Fi | Connects the ESP32 to the network |
| Messaging | MQTT or HTTP | Transfers readings to the cloud endpoint |
| Cloud/backend | IoT platform or API + database | Receives, validates, and stores measurements |
| Presentation | Web dashboard | Shows current readings, historical charts, and threshold alerts |

### 3. Data flow
1. The DHT22 measures temperature and humidity.
2. The ESP32 reads the sensor output at a fixed interval (for example, every 30 seconds).
3. The ESP32 packages the reading as JSON and sends it over Wi-Fi using MQTT or HTTP.
4. A cloud endpoint validates the message and stores it with a timestamp.
5. The dashboard retrieves the latest and historical measurements.
6. If temperature crosses a configured threshold, the dashboard can highlight the reading or issue an alert.

### 4. Example payload
```json
{
  "device_id": "room-01",
  "temperature_c": 27.4,
  "humidity_percent": 58,
  "timestamp": "2026-10-27T06:30:00Z"
}
```
These values are illustrative examples, not real sensor measurements.

### 5. Example use case
A room owner can check temperature and humidity remotely. Historical charts can help identify rooms that become too warm, while threshold alerts can prompt ventilation or cooling.

### 6. Security and reliability considerations
- Use authenticated device credentials and encrypted transport (TLS/HTTPS or MQTT over TLS).
- Keep credentials out of public source code.
- Validate incoming values and reject malformed messages.
- Buffer readings temporarily if the network is unavailable, then retry transmission.
- Monitor device connectivity and timestamp readings consistently.

### 7. Limitations and assumptions
This is an architecture proposal only. No physical sensor, ESP32, cloud database, or live dashboard has been connected. MQTT/HTTP and the cloud platform are design choices; the implementation would depend on the selected service.

### 8. Architecture diagram
See [`iot-system-architecture.svg`](iot-system-architecture.svg).<img width="2268" height="1144" alt="iot-system-architecture" src="https://github.com/user-attachments/assets/d6b1216d-0d3f-4618-84d6-1aaf6fe7e545" />


### 9. Learning outcomes
- Identified the sensing, edge, connectivity, cloud, and application layers.
- Mapped data movement from sensor to dashboard.
- Considered basic security, reliability, and data validation.

---
Prepared for the SWYNEX internship task. Update this document if the task mentor specifies a preferred cloud platform or protocol.
