# Descriptions for standardized json output

This readme describes the json output schema that we standardized for AITRIOS AI model. Current json output schema is mainly for DNN object detection and post-processing for smart city use-case such as traffic counting and curb management.
- frame_output_schema.json: output schema for frame-based output

----

### frame_output_schema.json

#### config
| Field Name            | Required  | Data Type | Description |
|-----------------------|-----------|-----------|-------------|
| source_type           |   Y       | string    | Source type for data |
| camera_id             |   Y       | integer   | Camera id |
| video_file_name       |   N       | string    | Video file name; leave as 'null' if it's online processing |
| total_image_frames    |   N       | integer   | The number of total images for processing; leave as -1 if it's online processing |
| input_tensor_height   |   Y       | integer   | Input tensor size (height) |
| input_tensor_width    |   Y       | integer   | Input tensor size (width) |
| output_tensor_height  |   Y       | integer   | Output tensor size (height) |
| output_tensor_width   |   Y       | integer   | Output tensor size (width) |
| traffic_counting      |   N       | array of [LineString](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.2) or [Polygon](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.3)     | Boundary coordinates for traffic counting |
| bike_counting         |   N       | array of [LineString](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.2) or [Polygon](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.3)  | Boundary coordinates for bike counting |
| pedestrian_counting   |   N       | array of [LineString](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.2) or [Polygon](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.3)    | Boundary coordinates for pedestrian counting |
| parking_zone          |   N       | array of [Polygon](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.3)     | Parking zone coordinates |

#### output
| Field Name | Required  | Data Type | Description |
|------------|-----------|-----------|-------------|
| frame_id  |   Y       | integer    | Unique identifier for the frame |
| timestamp  |   N       | string    | The timestamp of the frame in ISO 8601 format |
| object_ids   |   Y       | array of integer   | List of detected objects in the frame |
| object_bboxes    |   Y       | array     | Bounding box coordinates of the detected object [x1, y1, x2, y2] |
| object_class  |   Y       | array of string    | Type of the detected object (supported objects: "pedestrian", "bicycle", "cargo_bicycle", "car", "scooter", "moped", "motorcycle", "truck", "van", "freight", "other", "unspecified")|
| object_scores       |   Y       | array of number    | Confidence score of the detected object |
| traffic_counting       |   N       | array of integer    | The total number of vehicle that passes the counting boundary |
| bike_counting |   N       |  array of integer     | The total number of bike that passes the counting boundary |
| pedestrian_counting |   N       |  array of integer     | The total number of pedestrian that passes the counting boundary |
| parking_status |   N       | object     | Parking status ([more details](https://github.com/smart-camera-engagement/eval-ai-models/tree/main/smart_city_json_output#more-details-on-parking-status)) |

##### More details on parking status
| Field Name | Required  | Data Type | Description |
|------------|-----------|-----------|-------------|
| occupied |   Y       | array of boolean     | Parking status for each parking zone in the current frame (true or false) |
| parking_dwell_time |   Y       | array of integer     | Parking dwell time for each parking zone (unit is seconds) |
| double_parking_status |   N       | object    | Double parking status ([more details](https://github.com/smart-camera-engagement/eval-ai-models/tree/main/smart_city_json_output#more-details-on-double-parking-status)) |

##### More details on double parking status
| Field Name | Required  | Data Type | Description |
|------------|-----------|-----------|-------------|
| status |   Y       | boolean     | Double parking status in the current frame (true or false) |
| double_parking_dwell_time |   N       | integer     | Double parking dwell time in the current frame (unit is seconds) |
| vehicle_blocked_lane_types |   N       | [LaneType](https://github.com/openmobilityfoundation/curb-data-specification/tree/main/events#lane-type)    | Type of lane blocked by the vehicle performing the event. |
| double_parking_location |   N       | array of [Point](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.1) or [Polygon](https://datatracker.ietf.org/doc/html/rfc7946#appendix-A.3)    | Double parking location coordinates |


----
### Version
|   Version  |   Date    | Description |
|------------|-----------|-------------|
| 1.0.0      | 11/6/2024 |First version created for DNN object detection output and smart city use-case|