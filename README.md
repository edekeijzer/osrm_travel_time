# OSRM Travel Time sensor for Home Assistant (osrm_travel_time)
Shamelessly copied from https://github.com/eifinger/open_route_service and modified to use the https://pypi.org/project/osrm-py/ client for OSRM for making completely self-contained travel times in possible in Home Assistant.
You can specify origin and destination by either a device_tracker, zone or person entity_id or by latitude/longitude coordinates.

## Configuration
```yaml
sensor:
  - platform: osrm
    name: Travel home by bike
    server: 'https://route.example.com'
    profile: bike
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
`profile` | `string` | `false` | Enter a profile name here, which exists in your OSRM server. The default is `car`.
`unit_system` | `string` | `false` | You can choose between `metric` or `imperial`. Defaults to follow your Home Assistant configuration.
`scan_interval` | `integer` | `false` | "Defines the update interval of the sensor in seconds. Defaults to 300 (5 minutes)."

## Bugs and support
If you find a bug or have a feature request, please let me know in the issue tracker or fork the plugin, add your feature and create a Pull Request. Please note that I do not provide any support on OSRM deployment or configuration, please see the [OSRM wiki](https://github.com/Project-OSRM/osrm-backend/wiki) for that.