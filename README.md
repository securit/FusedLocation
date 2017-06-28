# Titanium Android FusedLocation 

 Summary
---------------
FusedLocation is an open-source project to support the Android's new LocationRequest in Appcelerator's Titanium Mobile.

⚠ Axway Titanium are implementing this feature (FusedLocation for Android) part of the Ti SDK. You can watch it here: https://jira.appcelerator.org/browse/TIMOB-20522

Requirements
---------------
  - Titanium Mobile SDK 6.1.0.GA or later
  - Android 2.3 or later

Download + Setup
---------------

### Download
  * [Stable release](https://github.com/yozef/FusedLocation/releases)

### Setup
Unpack the module and place it inside the `modules/android/` folder of your project.
Edit the modules section of your `tiapp.xml` file to include this module:
```xml
<modules>
    <module platform="android">ca.underlabs.fusedlocation</module>
</modules>
```

Features
--------
#### Start Location (location updates event)

```javascript
var FusedLocation = require('ca.underlabs.fusedlocation');

FusedLocation.startGeoLocation({
    success: function(e) {
        // returns similar to iOS location event: 
        // {"type":"location","success":true,"provider":"fused",
        //      "coords":{"bearing":0,"latitude":40.4688283,"timestamp":1486002223000,"speed":0,"accuracy":1,"longitude":-72.74637}}
        Ti.API.info(JSON.stringify(e)); 
        // handleLocation(e); // create a function that handles the event for both platforms!
    },
    error: function(e) {
        Ti.API.info('Android GeoLocation Fusion Error :(');
        Ti.API.info(JSON.stringify(e));
    }
});

```

#### Stop Location (save on battery consumption when not needed)
```javascript
FusedLocation.stopGeoLocation();
```

### Defaults
By Default in the code (hardcoded - pull requests welcomed):
- PRIORITY is set to 100 (meaning GPS - Most Accurate)
- DISTANCE_FILTER is set to 5 meters (location event updates when accelerometers senses that 5 meters have been traversed)

If Distance Filter is triggered (example driving very fast), below are handled by:
- FASTEST_UPDATE_FREQ is set to 1 second (every 1 sec at fastest)
- INTERVAL is set to 5 second (at latest)


Usage with ti.map
------------------
Make sure to delete in `/1.2.2/lib/` these 2 jars: 
- `classes-base.jar` and 
- `classes-basement.jar`

Since they’re already in ti.map, and just leave `classes.jar` (which holds com.google.android.gms.location)

### Build
If you want to build the module from the source, you need to check some things beforehand:
- You'll need all three .jar files in your build path
- With Ti >= 6.0.0, use within android folder `appc run --build-only`


TODO: These are Hardcoded - PullRequests are Welcomed, and I will try to update it so that these can be passed from Ti App part of `startGeoLocation`.

#### TODO
[ ] Allow params to be passed to `startGeoLocation` for: `priority`, `distanceFilter`, `fastestInterval` and `interval`

Contributing
---------------
Code contributions are greatly appreciated, please submit a new pull request!
