# WZDx Specification v4.0
Released December 2021

WZDx version 4.0 implements clean up and small additions in functionality to the WZDx feed and adds definitions for two new feeds, the [SwzDeviceFeed](/spec-content/objects/SwzDeviceFeed.md) and [RoadRestrictionFeed](/spec-content/objects/RoadRestrictionFeed.md). Until version 4.0, the WZDx specification defined only one feed, the [WZDxFeed](/spec-content/objects/WZDxFeed.md).

## Features
- Add the following values to the [VehicleImpact](/spec-content/enumerated-types/VehicleImpact.md) enumerated type:
    - `some-lanes-closed-merge-left`
    - `some-lanes-closed-merge-right`
    - `all-lanes-open-shift-left`
    - `all-lanes-open-shift-right`
    - `some-lanes-closed-split`
    - `flagging`
    - `temporary-traffic-signal`
- Allow restrictions with a value and unit to be provided at the road event level; specifically:
    - Rename the LaneRestrictionUnit enumerated type to [UnitOfMeasurement](/spec-content/enumerated-types/UnitOfMeasurement.md).
    - Rename the RoadRestriction enumerated type to [RestrictionType](/spec-content/enumerated-types/RestrictionType.md).
    - Rename the LaneRestriction object to [Restriction](/spec-content/objects/Restriction.md) and remove the `lane_restriction_` prefix from its properties.
    - Rename the [Restriction](/spec-content/objects/Restriction.md) object `units` property to `unit`.
- Add values `parking` and `median` to the [LaneType](/spec-content/enumerated-types/LaneType.md) enumerated type.
- Define a new data feed, the [RoadRestrictionFeed](/spec-content/objects/RoadRestrictionFeed.md) and [RestrictionRoadEvent](/spec-content/objects/RestrictionRoadEvent.md) to enable providing a feed of restrictions on roadways, such as bridge clearances.
- Define a new data feed, the [SwzDeviceFeed](/spec-content/objects/SwzDeviceFeed.md), to enable equipment vendors and manufacturers to provide high-level information about deployed field devices in work zones. A `SwzDeviceFeed` contains a new feature type, the [FieldDeviceFeature](/spec-content/objects/FieldDeviceFeature.md), which contains information about a specific type of field device. The following field devices are defined in WZDx v4.0:
    - `ArrowBoard`: An electronic, connected arrow board which can display an arrow pattern to direct traffic.
    - `Camera`: A camera device deployed in the field, capable of capturing still images.
    - `DynamicMessageSign`: An electronic traffic sign deployed on the roadway, used to provide information to travelers.
    - `FlashingBeacon`: A flashing beacon light of any form (e.g. trailer-mounted, vehicle), used to indicate something or capture driver attention.
    - `HybridSign`: A hybrid sign that contains static text (e.g. on an aluminum sign) along with a single electronic message display, used to provide information to travelers.
    - `LocationMarker`: Describes any GPS-enabled ITS device that is placed at a point on a roadway to dynamically know the location of something (often the beginning or end of a work zone).
    - `TrafficSensor`: A traffic sensor deployed on a roadway which captures traffic metrics (e.g. speed, volume, occupancy) over a collection interval.
- Rename the `workers_present` property on the [WorkZoneRoadEvent](/spec-content/objects/WorkZoneRoadEvent.md) object to  `worker_presence`; change the type from "boolean" to a new [WorkerPresence](/spec-content/objects/WorkerPresence.md) object which enables providing more nuanced information about worker presence in work zones.

## Refactoring
- Separate the v3.1 RoadEvent object into [RoadEventCoreDetails](/spec-content/objects/RoadEventCoreDetails.md) (details that are shared by all specific types of road events) and specific types of road events ([WorkZoneRoadEvent](/spec-content/objects/WorkZoneRoadEvent.md), [DetourRoadEvent](/spec-content/objects/DetourRoadEvent.md), and [RestrictionRoadEvent](/spec-content/objects/RestrictionRoadEvent.md)) which each contain the `RoadEventCoreDetails` via a `core_details` property; update the [RoadEventFeature](/spec-content/objects/RoadEventFeature.md) `properties` property to be one of the specific road events types.
- Move the `location_method` property from the [FeedDataSource](/spec-content/objects/FeedDataSource.md) object to the [WorkZoneRoadEvent](/spec-content/objects/WorkZoneRoadEvent.md) object.
- Change the `reduced_speed_limit` property on the [WorkZoneRoadEvent](/spec-content/objects/WorkZoneRoadEvent.md) to `reduced_speed_limit_kph`; change its type from "integer" to "number" and clarify that the value should be in kilometers per hour.
- Deprecate the `lane_number` property on the [Lane](/spec-content/objects/Lane.md) object.
- Deprecate the `lrs_type` and `lrs_url` properties on the [FeedDataSource](/spec-content/objects/FeedDataSource.md) object.
- Remove the deprecated value `alternating-one-way` from the [LaneStatus](/spec-content/enumerated-types/LaneStatus.md) enumerated type.
- Remove the following deprecated properties from the road event (RoadEvent in previous versions; [WorkZoneRoadEvent](/spec-content/objects/WorkZoneRoadEvent.md) and [RoadEventCoreDetails](/spec-content/objects/RoadEventCoreDetails.md) in 4.0):
    - `road_event_id`
    - `road_number`
    - `road_name`
    - `total_num_lanes`
- Remove the following deprecated values from the [LaneType](/spec-content/enumerated-types/LaneType.md) enumerated type: 
    - `left-lane`
    - `right-lane`
    - `middle-lane`
    - `center-lane`
    - `right-shoulder`
    - `left-shoulder`
    - `right-second-exit-ramp`
    - `left-second-exit-ramp`
    - `right-entrance-exit-ramp`
    - `left-entrance-exit-ramp`
    - `hov-lane`
    - `alternating-flow-lane`
    - `reversible-lane`
    - `right-entrance-lane`
    - `left-entrance-lane`
    - `left-entrance-ramp`
    - `right-merging-lane`
    - `left-merging-lane`
    - `right-second-entrance-ramp`
    - `left-second-entrance-ramp`
- Require the `road_names` property on the [RoadEventCoreDetails](/spec-content/objects/RoadEventCoreDetails.md).
- Require the `id` property on the [RoadEventFeature](/spec-content/objects/RoadEventFeature.md).
- Refine the [LaneType](/spec-content/enumerated-types/LaneType.md) enumerated type; specifically:
    - Rename `lane` to `general`.
    - Remove `right-turning-lane` and `left-turning-lane`.
    - Remove `right-exit-lane` and `left-exit-lane`.
    - Add `exit-lane`.
    - Remove `right-exit-ramp` and `left-exit-ramp`.
    - Add `exit-ramp`.
    - Remove `right-entrance-ramp` and `left-exit-ramp`.
    - Add `entrance-ramp`.
    - Add `entrance-lane`.
- Deprecate the `location_verify_method` property on the [FeedDataSource](/spec-content/objects/FeedDataSource.md).
- Update the [SpatialVerification](/spec-content/enumerated-types/SpatialVerification.md) enumerated type value descriptions to clarify that verified work zone locations should use a GPS enabled device.

# WZDx Specification v3.1
Released April 2021

Following the major v3.0 release, the changes for the v3.1 release were developed with the goal enhancing and cleaning up the specification without making major changes or breaking backwards compatibility. Thus, in v3.1 many enumerated type values or object properties were deprecated rather than removed. Most if not all of these deprecated values will be removed in the next major release.

This repository was also renamed from `jpo-wzdx` to `wzdx` on 2021-04-05. All links pointing to `jpo-wzdx` will automatically redirect to the new URL. 

## Features
* Add `local-access-only` restriction
* Add `license` property to the `RoadEventFeedInfo` object

## Refactoring
* Refactor `LaneType` enumerated type to deprecate values that can be determined from other properties of the Lane object, such as `order`, `status`, and `lane_restrictions`
* Add value `alternating-flow` to `LaneStatus` enumerated type and deprecate `alternating-one-way`
* Add `road_names` property to the `RoadEvent` object and deprecate `road_name` and `road_number`
* Deprecate the `total_num_lanes` property on the `RoadEvent` object as the `RoadEvent`'s `lanes` array can be used to determine the number of lanes

## Fixes
* Add optional `bbox` property to allow providing a [GeoJSON Bounding Box](https://tools.ietf.org/html/rfc7946#section-5) for the `WZDxFeed` and `RoadEventFeature` objects
* Add an `id` property to the `RoadEventFeature` object for providing the a road event's identifier to better follow [GeoJSON ID recommendations](https://tools.ietf.org/html/rfc7946#section-3.2)

# WZDx Specification v3.0
Released September 2020

## Features
* Restrict `version` format to `major.minor` and enforce via v3.0 JSON schema
* Add `order` property to Lane object to indicate a lane's position in sequence on the roadway
* Remove `lane_edge_reference` and standardize on counting lanes from the left side of the roadway
* Add `event_type` property to the RoadEvent object and new **EventType** enumerated type with the values `work-zone` and `detour`, to support adding detour information (and more in the future)
* Add **Relationship** object (one per RoadEvent) to enable describing relationships (hierarchical and sequential) between road events and other non-WZDx entities (such as a work zone phase or project)
* Add **RoadEventDataSource** object to allow specifying multiple data sources within a single feed
* Streamline **metadata** (previously given in an external file, by URL) and add relevant fields to the **RoadEventFeedInfo** and **RoadEventDataSource** objects

## Fixes
* Require `restriction_type` if providing a lane-level restriction
* Change **Spatial Verification Enumerated Type** and **Time Verification Enumerated Type** values to be all lowercase
* Remove all plural or nonsensical lane types from the **Lane Type Enumerated Type** and clarify that each WZDx lane should represent a *single* lane on the roadway

# WZDx Specification v2.0
Released January 2020

This release includes the first set of major changes to the specification. 

## Features
* Added new data tables to accommodate [mobility impact and lane level impacts/restrictions](https://github.com/usdot-jpo-ode/wzdx/pull/57) (i.e., closures and restrictions). The new lane-level information, as well as overall vehicle impact fields, allowing IOOs new flexibility in communicating impacts and mobility restrictions of a work zone.
* Added a new [Types of Work table](https://github.com/usdot-jpo-ode/wzdx/pull/59) to provide specific information on the types of work being performed at a work zone. This enumerated table categorizes the type of work and indicates if construction in a work zone will cause any architectural changes to the roadway. This information will support keeping the maps used by autonomous vehicles up to date.

## Refactoring
* [Required GeoJSON formatting](https://github.com/usdot-jpo-ode/wzdx/pull/53) of a WZDx feed. GeoJSON is a data interchange format based on JavaScript Object Notation (JSON) designed to exchange geospatial data. Since feeds can be used with existing validation, mapping, and visualizations tools, requiring GeoJSON will improve accessibility of work zone data activity to producers and consumers.
* Converted the “common core” data dictionary into a [relational data model](https://github.com/usdot-jpo-ode/wzdx/pull/54) with road event tables featuring new geometry-specific data elements. This conversion permits more efficient organization of the data elements for each work zone and supports a flexible, scalable data model.
  
# [WZDx Specification v1.1](https://github.com/usdot-jpo-ode/wzdx/tree/v1.1)
Released September 2018

Initial release. This version served as a first step in providing a standard work zone data activity framework. This version of the specification focused on “common core” data concepts which are defined as data elements needed for most work zone data use cases. The specification included data elements that data producers were already producing as well as those that may not currently be produced.
