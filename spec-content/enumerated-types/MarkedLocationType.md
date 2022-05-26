# MarkedLocationType Enumerated Type
The `MarkedLocationType` enumerated type describes options for what a [MarkedLocation](/spec-content/objects/MarkedLocation.md) can mark, such as the start or end of a road event.

## Values
Value | Description
--- | ---
`afad` | An automatic flagger assistance device.
`flagger` | A human who is directing traffic.
`lane-shift` | A lane shift.
`lane-closure` | One or more lanes are closed.
`road-event-start` | The start point of a road event.
`road-event-end` | The end point of a road event.
`work-zone-start` | The start point of a work zone.
`work-zone-end` | The end point of a work zone.
`temporary-traffic-signal` (DEPRECATED) | A temporary traffic signal. *This property will be removed in a future release; use [TrafficSignal](../objects/TrafficSignal.md].*

## Used By
Property | Object
--- | --- 
`type` | [MarkedLocation](/spec-content/objects/MarkedLocation.md)