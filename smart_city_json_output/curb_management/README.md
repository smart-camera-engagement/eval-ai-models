# Descriptions for json output schema of curb management use-case

This readme describes the json output schema for curb management that follows [Curb Data Specification (CDS)](https://github.com/openmobilityfoundation/curb-data-specification/tree/main). CDS events API 

- [curb_event_output_schema.json](https://github.com/smart-camera-engagement/eval-ai-models/blob/main/smart_city_json_output/curb_management/curb_event_output_schema.json): output schema for event-based output
- [curb_event_output_sample.json](https://github.com/smart-camera-engagement/eval-ai-models/blob/main/smart_city_json_output/curb_management/curb_event_output_sample.json): output sample
----

### curb_event_output_schema.json
curb_event_output_schema.json file consists of 'events' which is an array of curb event objects.

#### 'events' object
| Field Name            | Required  | Data Type | Description |
|-----------------------|-----------|-----------|-------------|
| event_id           |   Y       | integer    | Unique identifier of the event that occurred. |
| event_type         |   Y       | string ([EventType](https://github.com/openmobilityfoundation/curb-data-specification/tree/main/events#event-type))   | The event_type that happened for this event. |
| event_purpose      |   Y       | string ([EventPurpose](https://github.com/openmobilityfoundation/curb-data-specification/tree/main/events#event-purpose))   | General curb usage purpose that the vehicle performed during the event. Required for sources capable of determining activity type for relevant event_types. |
| event_location     |   Y       | object   | fds |
| event_time         |   Y       | string ([Timestamp](https://github.com/openmobilityfoundation/curb-data-specification/blob/main/general-information.md#timestamp))  | Time at which the event occurred. |
| event_publication_time    |   Y       | string ([Timestamp](https://github.com/openmobilityfoundation/curb-data-specification/blob/main/general-information.md#timestamp))  | Time at which the event became available for consumption by this API. |
| curb_zone_id  |   Y       | string   | ID of the Curb Zone where the event occurred.  |
| curb_area_ids   |   Y       | array of string   | IDs of the Curb Area where the event occurred. Since Curb Areas can overlap, an event may happen in more than one. |
| curb_space_id      |   Y       | string     | ID of the Curb Space where the event occurred. |
| object_id         |   Y       | integer  | Id of the vehicle that occurs the event |
| vehicle_type   |   Y       | string ([VehicleType](https://github.com/openmobilityfoundation/curb-data-specification/tree/main/events#vehicle-type))   | Type of the vehicle that performed the event.  |
| vehicle_blocked_lane_types          |   N       | array of [LaneType](https://github.com/openmobilityfoundation/curb-data-specification/tree/main/events#lane-type)    | Type(s) of lane blocked by the vehicle performing the event. If no lanes are blocked by the vehicle performing the event, the array should be empty. |

----
### Version
|   Version  |   Date    | Description |
|------------|-----------|-------------|
| 1.0.0      | 11/6/2024 | First version created for SJ curb management |