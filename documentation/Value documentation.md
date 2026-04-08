# Value Documentation

This page describes how to document values in the SDHSS ecosystem.

## Dates

### Shortcut for documenting dates

crm-sup:C39 Standard Date-Time
Expressed in the form of strings, based on the ISO and XSD format, e.g.: '2001-05-23T08:20:00+08:00'

Dates are defined in the Julian calendar until Thursday 4 October 1582 and continue in the Gregorian calendar from the next day, which was the Friday 15 October 1582. No Gregorian proleptic system is allowed before the 15 October 1582 and no Julian calendar dates are allowed after this date.

### Full paths for documenting dates

While most of cases can be handled with the shortcut `crm-sup:C39 Standard Date-Time`, the documentation of time in specific domains, such as date in a different calendar or other reference systems (for exampple in Ancient Egypt), requires a more complex model.

A central entity, labelled `sdh-xx:CX Temporal Position`, as subclass of `sdh:C5 Abstract Region`, documents the position in an abstract and conceptual space of time defined by a conventionally defined reference system. This class is equivalent to `time:TemporalPosition` in the time ontology.

This reference system is documented with the class `sdh-xx:CX Temporal Reference System`, as subclass of `sdh:C40 Intentional Set` (?), that specifies the Reference System or Calendar. This class is equivalent to `time:GeneralDateTimeDescription`?

The class `sdh-xx:CX Temporal Position` would then be linked to a Time Primitive with a property `sdh-xx:PX has date`.

Questions:
- Is `time:GeneralDateTimeDescription` realy equivalent to `sdh-xx:CX Temporal Reference System`?
- Should the Temporal Position be a Time Span? Or rather a single point in time, and the properties sdh-short P3 begins after, P4 begins on, etc. should still be used to link a Temporal Entity with a Temporal Position?

## Geo-coordinates

### Shortcut in a specific system

Similar to the documentation of dates, a shortcut linking an instance of `sdh:C13 Geographical Place` with a string containing the geo-coordinate in a standard format would be needed.

This means the creation of a specific subclass of `crm:E94 Space Primitive`, that could be labeled `crm-sup:CX Standard Geocoordinates`. Those primitive values must follow a strict standard

Questions:
- Should the string document a *single point*? Or would it be possible to describle multiple shapes, following the WKT standard?.
  - With a *single point*, the string of the primitive `crm-sup:CX Standard Geocoordinates` would be `x,xxx y,yyy`.
  - With different shapes, the primitive value would be `point (x.xx y.xx)`, `linestring (x.xx y.xx, x.xx y.xx, x.xx y.xx)`, etc. This implies that users have to specify the geometric shape.
- Which Standard should be used? It would be best to use the WGS84.

### Full path for documenting different shapes in different systems

To express a more complex description of geocoordinates, as well as specify coordinate systems, a more develop pattern is needed.

First, the use of the class `crm:E93 Presence` allows the description of the spatial extent at a given temporal position. Instances of `sdh:C13 Geographical Place` (but also other instances of `crm:E18 Physical Thing` or `crm:E4 Period`) could be linked to one or more instances of the class `crm:E93 Presence` with the property `crm:P195 was presence of` or `crm:P166 was presence of`.

The instance of `crm:E93 Presence` would then be linked to an instance of `crm:E53 Place` with the property `crm:P167 was within`.

> In Geovistory it seems that from the Presence, the property `crm:P167 was within` links directly to a string, that has as a value `<http://www.opengis.net/def/crs/EPSG/0/4326>POINT(x.xx y.yy)"^^geo:wktLiteral`.

The class `crm:E53:Place`, a subclass of `sdh:C5 Abstract Region` is analogous to Temporal Position, in the sens that "a Place can be determined by combining a frame of reference and a location with respect to this frame".

The instance of the class `crm:E53:Place` can then be associated to a coordinate system and its value expressed with a space primitive:
- The Coordinate System can be documented with an instance of a new class `sdh-xx:CX Geocoordinate System`, linked with a property `sdh-xx:PX within geocoordinate system`.
- The value can be expressed from the instance of `crm:E53:Place` to a space primitive (or a subclass of `crm:E94 Space Primitive`) through the property `crm:P171 at some place within` (or should it be a specific property?).

Questions:
- How to express the WKT standard? Should the place have a Type "Point", "LineString", "Polygon", etc., or the type expressed in the space primitive directly, such as `point (x.xx y.xx)`, `linestring (x.xx y.xx, x.xx y.xx, x.xx y.xx)`.

### How it's done in WissKI

How Geographical data is managed in WissKI?

## Weights and measures

Measures

## Texts

Quill?

This is still to define

## URIs, External Identifiers and URLs

`owl:sameAs`
`crm-sup:P20 same as external identifier`

Should we have another shortcut from any entity (domain `crm:E1 CRM Entity`), to a URL? such as `sdh-short:PX has web page`

The longer path is having the webpage documented as an instance of `lrmoo:F2 Expression` (? another class? create a new class equivalent to `geov:C4 Web Request`?). This webpage would be about the entity, and the webpage available at a specific address.

## Appellation and labels

Shortcuts:
`sdh-short:P9 has standard label`
`sdh-short:P10 has alternative label`

The longer path is with `sdh:C11 Appellation in a Language`. Do we need anything else with the Appellation in a Language profile?