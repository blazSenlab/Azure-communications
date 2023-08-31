### Detailed Overview of Communication Protocols Supported by Azure IoT Hub

#### Protocols Supported
1. **MQTT**
2. **MQTT over WebSockets**
3. **Advanced Message Queuing Protocol (AMQP)**
4. **AMQP over WebSockets**
5. **HTTPS**

#### Pros and Cons

##### MQTT
- **Pros**: 
  - Efficient for both the device and IoT Hub.
  - Supports server push for immediate message delivery.
  - Good for low-resource devices.
- **Cons**: 
  - Limited feature support in IoT Hub.
  - Not suitable for field gateway scenarios requiring multiple device identities.

##### MQTT over WebSockets
- **Pros**: 
  - Efficient and supports server push.
  - Can traverse networks closed to non-HTTPS protocols.
- **Cons**: 
  - Limited feature support.
  - Not suitable for field gateways.

##### AMQP
- **Pros**: 
  - Supports connection multiplexing across devices.
  - Suitable for field gateways.
- **Cons**: 
  - Larger library footprint.
  - May have issues in networks closed to non-HTTPS protocols.

##### AMQP over WebSockets
- **Pros**: 
  - Supports connection multiplexing.
  - Can traverse networks closed to non-HTTPS protocols.
- **Cons**: 
  - Larger library footprint.

##### HTTPS
- **Pros**: 
  - Works in all network environments.
  - Suitable for rarely connected devices.
- **Cons**: 
  - Inefficient for server push.
  - Devices should poll for messages every 25 minutes or more to avoid throttling.

#### Recommendations
- **MQTT/MQTT over WebSockets**: Use on all devices that don't require connection to multiple devices over the same TLS connection.
- **AMQP/AMQP over WebSockets**: Use on field and cloud gateways to take advantage of connection multiplexing.
- **HTTPS**: Use for devices that can't support other protocols.

#### Additional Considerations
- **Port Numbers**: 
  - MQTT: 8883
  - MQTT over WebSockets: 443
  - AMQP: 5671
  - AMQP over WebSockets: 443
  - HTTPS: 443

### Suggested Protocol for Your Use Case

Given that you will be sending data to Azure via nRF52840, which is a low-resource device, **MQTT** would be a suitable choice for the following reasons:

1. **Efficiency**: MQTT is efficient for both the device and IoT Hub.
2. **Server Push**: Supports immediate message delivery from IoT Hub to the device.
3. **Low Resource Requirement**: MQTT libraries have a smaller footprint, making it suitable for low-resource devices like nRF52840.
