# node-red-rapt-pull
Simple node to pull data from RAPT cloud for integration into Node-RED flows.

RAPT Pill is a floating digital hydrometer and thermometer produced by KegLand.
It pushes periodic telemetry data to the RAPT cloud via WiFi or indirectly via Bluetooth through a compatible KegLand device.

The rapt-pull node uses the RAPT API v1 to request device or telemetry information from the RAPT cloud so that it can be integrated into a Node-RED flow.

Currently the following API endpoints are supported 

```
/api​/Hydrometers​/GetHydrometers
/api​/Hydrometers​/GetHydrometer
/api​/Hydrometers​/GetTelemetry
```
Each instance of the rapt-pull node is configured to invoke one of the supported endpoints.

When configured for GetHydrometers, it will return an array of objects containing details for all hydrometers registered against your RAPT account.  
When configured for GetHydrometer, it will return an object containing details about a single hydrometer.  
When configured for GetTelemetry, it will return an array of objects containing telemetry information for a specific time period.  

By chaining node instances together it is very easy to create a flow to get exactly the information you would like.

For example, to get all new telemetry information hourly, you could wire an inject node, set to repeat every hour, into a rapt-pull node configured for GetHydrometers, then wire the output of that node to another rapt pull node configured for GetTelemetry, as shown in the example below. In this configuration, the node configured for GetTelemetry will retrieve the telemetry data for the period since it was last invoked.

![example1](./readme/example1.png?raw=true)

Alternatively, you could get telemetry information for a specific time period by inserting a change node to set the start and end properties of the message before the rapt-pull node configured for GetTelemetry, as shown below.

![example2](./readme/example2.png?raw=true)


The example flows above are included in the node-red-rapt-pull package and available for import into your node red instance.
