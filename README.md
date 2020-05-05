# osrm_travel_time
Shamelessly copied from https://github.com/eifinger/open_route_service and modified to use the https://pypi.org/project/osrm-py/ client for OSRM for making completely self-contained travel times in possible in Home Assistant.

## Configuration
```yaml
sensor:
  - platform: osrm
    name: Travel home by bike
    server: 'https://route.example.com'
    profile: bicycle
    origin_entity_id: person.my_person
    destination_entity_id: zone.home
  - platform: osrm
    name: Travel home by car
    server: 'http://localhost:5000'
    profile: car
    origin_entity_id: device_tracker.my_device
    destination_entity_id: zone.home
```
## Configuration options
Key | Type | Required | Description
-- | -- | -- | --
`server` | `string` | `true` | Your OSRM server without path. The `profile` option will be included in the path.
`origin_latitude` | `string` | `true` | The starting latitude for calculating travel distance and time. Must be used in combination with origin_longitude. Cannot be used in combination with origin_entity_id
`origin_longitude` | `string` | `true` | The starting longitude for calculating travel distance and time. Must be used in combination with origin_latitude. Cannot be used in combination with origin_entity_id
`destination_latitude` | `string` | `true` | The finishing latitude for calculating travel distance and time. Must be used in combination with destination_longitude. Cannot be used in combination with destination_entity_id
`destination_longitude` | `string` | `true` | The finishing longitude for calculating travel distance and time. Must be used in combination with destination_latitude. Cannot be used in combination with destination_entity_id
`origin_entity_id` | `string` | `true` | The entity_id holding the starting point for calculating travel distance and time. Cannot be used in combination with origin_latitude / origin_longitude
`destination_entity_id` | `string` | `true` | The entity_id holding the finishing point for calculating travel distance and time. Cannot be used in combination with destination_latitude / destination_longitude
`name` | `string` | `false` | A name to display on the sensor. The default is "OSRM Travel Time".
`profile` | `string` | `false` | You can choose between: `car`, `bicycle` or `foot`. The default is `car`.
`unit_system` | `string` | `false` | You can choose between `metric` or `imperial`. Defaults to `metric` or `imperial` based on the Home Assistant configuration.
`scan_interval` | `integer` | `false` | "Defines the update interval of the sensor in seconds. Defaults to 300 (5 minutes)."
