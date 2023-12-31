[**UDMI**](../../) / [**Docs**](../) / [**Specs**](./) / [Compliance](#)

# UDMI Compliance

This is an overview of what it means for a device to be "UDMI Compliant."
There are several different facets to UDMI, each providing a different
bit of functionality, so the actual requirements will depend on the
intended function of the device.

* [_pointset_ telemetry](../messages/pointset.md), used for basic telemetry ingestion.
* [_writeback_ control](./sequences/writeback.md), used for on-prem device control.
* [_gateway_ proxy](gateway.md), used to proxy data for non-MQTT devices.
* [_system_ basics](../messages/system.md), used for general monitoring and logging.

The [Tech Primer](../tech_primer.md) gives a primer for smart-ready building assembly requirements

## Feature Buckets

The _feature buckets_ list classifies the defined functionality within the UDMI specification into
individual features and buckets. This aids in assessing levels or completeness of compliance of a
device and can be used for defining requirements.

*   **Enumeration**
    *   _`multi_enumeration`_ - ..
    *   _`empty_enumeration`_ - ..
    *   **Pointset**
        *   _`pointset_enumeration`_ - ..
    *   **Features**
        *   _`features_enumeration`_ - ..
    *   **Families**
        *   _`family_enumeration`_ - ..
*   **Discovery**
    *   **Scan**
        *   _`discovery_scan`_ - Rejects bad hash
*   **Endpoint**
    *   _`MQTT 3.1.1 support`_ - Device supports MQTT 3.1.1
    *   _`MQTT/TLS Support`_ - Device supports connection to an MQTT broker with TLS encryption and at least TLS v1.2 
    *   _`Server certificate validation`_ - Device validates MQTT broker server certificates
    *   _`Maintains Connection`_ - The device can connect and sustain a connection to the MQTT broker
    *   _`Network resumption reconnection`_ - Device reconnects to MQTT broker when connection is lost, or reattempts connection if connection attempts are unsuccessful
    *   _`Exponential backoff`_ - Device reconnects to MQTT broker when connection is lost, or reattempts connection if connection attempts are unsuccessful
    *   _`JWT `_ - Device is able to authenticate to an MQTT bridge using JWT credentials in the password and renew
    *   _`User configurable connection`_ - Connection parameters (including client ID, hostname, port, etc) are user configurable
    *   **Configuration**
        *   _`endpoint_connection_bad_hash`_ - Rejects bad hash
        *   _`endpoint_connetion_success_alternate`_ - Can successfully connect to alternate endpoint
        *   _`endpoint_connection_success_reconnect`_ - Reconnects to the new endpoint, after restart
        *   _`endpoint_connection_retry`_ - ..
*   **System**
    *   _`device_config_acked`_ - Device subscribes to the config topic with a QoS 1 and always publishes PUBACKs to the broker 
    *   _`State after configuration`_ - Device publishes state messages after receiving a config message
    *   _`system_last_update`_ - system.last_update field in state messages matches timestamp of last config message
    *   _`broken_config`_ - The device remains functional when receiving a config messages which is invalid at a core level (e.g. invalid JSON, missing fields required fields such as top level timestamp), retaining the previous config 
    *   _`extra_config`_ - The device remains functional when config messages contains fields which are not recognized by the device
    *   _`system_min_loglevel`_ - Configurable min log level for filtering published status/logging information
    *   _`system_hardware`_ - Hardware block is included and the contents match the physical hardware 
    *   _`system_software`_ - Software block in state messages is included, with keys and values automatically generated by the device matching the software versions installed
    *   _`valid_serial_no`_ - Serial number in state message matches physical hardware
    *   **Mode**
        *   _`system_mode_restart`_ - device restarts
    *   **Logging**
        *   _`system.config.receive`_ - Device publishes a logentry when it receives a config update
        *   _`system.config.parse`_ - Device publishes a logentry when it parses a config update
        *   _`system.config.apply`_ - Device publishes a logentry when it applies (accepts) a config update
        *   _`system.base.startup`_ - System startup events are logged
        *   _`system.base.ready`_ - System fully-ready events are logged
        *   _`system.base.shutdown`_ - System shutdown events are logged
        *   _`system.network.connect`_ - Network connection events are logged
        *   _`system.network.disconnect`_ - Network disconnection events are logged
        *   _`system.auth.login`_ - Successful logins to device application are logged
        *   _`system.auth.fail`_ - Failed authentication attempts to device application are logged
    *   **Metrics**
        *   _`publish`_ - Device publishes system metrics
        *   _`schema`_ - metrics valid with UDMI schema
        *   _`metrics_rate_sec`_ - Implements metrics_rate_sec to configure sample rate for metrics
*   **Pointset**
    *   _`Publish`_ - Publishes pointset event messages with a valid schema
    *   _`Datapoint mapping`_ - Mapping of UDMI data points to device-internal data points is through config messages, allowing points to be renamed
    *   _`Pointset Config`_ - Pointset is configured through UDMI, only publishing points which are in the config, and the points are in state 
    *   _`Offline buffering`_ - Telemetry events while device is offline are stored and published when connection is resumed
    *   _`pointset_sample_rate`_ - Sampling rate for the system, at which it should proactively send a complete pointset within the `pointset.sample_rate_min`, defined in the config message
    *   _`pointset_publish_interval`_ - Minimum time between pointset events is defined by `pointset.sample_limit_sec` in the config message
    *   **CoV**
        *   _`Partial updates`_ - Supports partial updates (with partial_update flag set to true)
        *   _`Configurable CoV Increment`_ - Configurable CoV increment per point through UDMI Config
        *   _`sample_limit_sec`_ - Limit sample sec

