<!-- docs/op/Insert_Geofence/README.md -->
# Insert_Geofence

> The creation of circular zones that can trigger different kind of alarms: alarms when entering and/or leaving, alarms when an activity takes more than x minutes in this zone or alarms when not in the zone before a certain date and time.
> - It is not possible to create polygone geofence via the web services, this needs to be done via TX-CONNECT.

## Version info
- Version 2 adds the option to create a geofence based on an existing POI.

## Request
\* is mandatory, \*\* Either GeoValidity date or ETADate need to be used

- [Login block](/op/loginblock.md)*
- GeofenceInsert: _InterfaceGeoFenceInsert V2_
	- Geozones: _array of IntefaceGoeZone V2_
		- Name: _string_
		- Position: _Position_
			- Longitude: _double_
			- Latitude: _double_
		- Radius: _int32_
		- DriverAlarmText: _string
		- PoiID: _int32_
	- Active*: _boolean_, set true, otherwise an inactive geofence is created
	- ETADate**: _DateTime_, generate an alarm when not in the zone by this date-time
	- GeoValidityDate**: _GeoValidityDate_, the period that the alarm is valid for
		- BeginDate*: _DateTime_, should not be in the passed
		- EndDate*: _DateTime_
	- Name*: _string_
	- DriverAlarmText: _string_, what text should be shown to driver when the alarm occurs. 
	- NotifyHomeBase: _boolean_, alarm for the backoffice (TX-CONNECT, Web service, ...)
	- NotifyDriverByBeep: _boolean_
	- NotifyOnce: _boolean_, the alarm will only be triggered once for each vehicle
	- GeoFenceDirection*: _enumGeofenceDirection_: ENTER, LEAVE, ENTER\_LEAVE, alarm upon entering or leaving or both
	- GeoZonePositive: _boolean_, true: zone colours red when vehicle is inside, otherwise green. false: vica-versa
	- RestrictedActivity: _ActivityPlace_, give an alarm when an activity takes longer than x minutes, if this is used than the GeoFenceDirection will be ignored.
		- ID: _int32_
		- Name: _string_
		- MaxTimeOfExecution: _int32_

## Response
Derived from result object, contains Errors and Warnings: See [result object](/op/resultobject.md)
- result: _InsertGeoFenceResult_
	- GeoFenceID: _int64_, unique id of the geofence, need to be stored to easily interpret alarms via [Get_AlarmMessages](/op/Get_AlarmMessages/)
	- GeoFenceName: _string_
	- GeoZones: _array of InsertGeoZoneResult_
		-  GeoZoneTNR: _int64_, unique id of the geozone, need to be stored to easily interpret alarms via [Get_AlarmMessages](/op/Get_AlarmMessages/)
		-  GeoZoneSeq: _int64_
		-  GeoZoneName: _string_

<!--## Example code
```csharp
	IWS.InterfaceVehicleSelection_V2 vehSel = new IWS.InterfaceVehicleSelection_V2();
	...
```-->

## Example xml
**Request**
```XML

```

**Response**
```XML

```