[![Download](https://api.bintray.com/packages/moreno/maven/mapviewpager/images/download.svg) ](https://bintray.com/moreno/maven/mapviewpager/_latestVersion)

# MapViewPager

Android library that connects ViewPager fragments with Google Maps markers and makes them work together.

![screenshot](http://i.imgur.com/tZ7wO4D.png) ![screenshot](http://i.imgur.com/mfbp5ps.png) ![screenshot](http://i.imgur.com/C4dVMU7.png)

Check out the **[sample apk](https://github.com/nitrico/MapViewPager/raw/master/MapViewPager.apk)** !

**Notice:**
* Not fully tested yet but it works perfectly on my Nexus 5 running Marshmallow.
* It is my first Android lib. Tips, suggestions or any other comments are welcome.


## Features

* Supports any amount of markers per fragment.
* Default camera position (for fragments with 0 or *more than 1* markers) automatically calculated.


## Download

##### Gradle

```gradle
repositories {
    maven {
        url  "http://dl.bintray.com/moreno/maven" 
    }
}

dependencies {
    compile 'com.android.support:appcompat-v7:23.1.1'
    compile 'com.google.android.gms:play-services-maps:8.4.0'
    compile 'com.github.nitrico.mapviewpager:mapviewpager:1.0.0'
}
```


## Usage

> Don't forget to add the right **permissions** and your Google Maps **API key** to your `AndroidManifest.xml`.

Create a ViewPager adapter extending from **MapViewPager.Adapter** or **MapViewPager.MultiAdapter** and override method
`CameraPosition getCameraPosition(int position)` or `List<CameraPosition> getCameraPositions(int position)` returning the markers camera position for each fragment. 

> To create a CameraPosition: `CameraPosition.builder().target(new LatLng(latitude, longitude)).zoom(zoom).build();`

Include the view in your xml layout
```xml
<com.github.nitrico.mapviewpager.MapViewPager
        android:id="@+id/mapViewPager"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:viewPagerWeight="1"
        app:mapWeight="1"
        app:mapGravity="1"
        app:mapOffset="56dp" />
```

Find the view in your activity then and call `mapViewPager.start(this, adapter)` or `mapViewPager.start(this, adapter, callback)` passing the AppCompatActivity (or FragmentActivity) and MapViewPager.Adapter (or MapViewPager.MultiAdapter) instances. You can also pass a **MapViewPager.Callback** instance to get notified when the GoogleMap object is created and working.

#### XML attributes

|Attribute|Format|Default|Description
|---|---|---|---|
|viewPagerWeight|integer|`1`|Weight of the viewpager in the layout|
|mapWeight|integer|`1`|Weight of the map in the layout|
|mapGravity|integer (0..3)|`1`|Position of the map in the layout: 0=left, 1=top, 2=right, 3=bottom|
|mapOffset|dimension|`56dp`|Map *padding* for multiple markers on the map|
|mapPaddingLeft|dimension|`0dp`|Left map padding|
|mapPaddingTop|dimension|`0dp`|Top map padding|
|mapPaddingRight|dimension|`0dp`|Right map padding|
|mapPaddingBottom|dimension|`0dp`|Bottom map padding|
|markersAlpha|float (0..1)|`0.4`|Opacity of markers when deactivated|

#### Public methods

###### MapViewPager

|MapViewPager|
|---|
|Return type|Method name|Arguments|
|---|---|---|
|`void`|`start`|`FragmentActivity, MapViewPager.AbsAdapter`|
|`void`|`start`|`FragmentActivity, MapViewPager.AbsAdapter, MapViewPager.Callback`|
|`GoogleMap`|`getMap`||
|`SupportMapFragment`|`getMapFragment`||
|`ViewPager`|`getViewPager`||
|`CameraUpdate`|`getDefaultPosition`||
|`List<List<Marker>>`|`getAllMarkers`||
|`Marker`|`getMarker`|`int`|
|`List<Marker>`|`getMarkers`||
|`Marker`|`getMarker`|`int, int`|
|`List<Marker>`|`getMarkers`|`int`|
|`List<List<Marker>>`|`getAllMarkers`||
|`CameraUpdate`|`getDefaultPosition`|`int`||
|`List<CameraUpdate`|`getDefaultPositions`||

###### MapViewPager.Callback
|Return type|Method name|Arguments|
|---|---|---|
|`void`|`onMapViewPagerReady`||


#### Builder

If you want more control on how to display the map and the ViewPager, for example to overlay one on the other, you can freely add a `<android.support.v4.view.ViewPager>` and a `<fragment class="com.google.android.gms.maps.SupportMapFragment">` to your activity layout and then and pass them to create the MapViewPager object using the **MapViewPager.Builder** class:

```java
MapViewPager mvp = new MapViewPager.Builder(this)   // this is Context
        .mapFragment(map)                           // map is SupportMapFragment
        .viewPager(viewPager)                       // viewPager is ViewPager
        .adapter(adapter)                           // adapter is MapViewPager.Adapter or MapViewPager.MultiAdapter
        .callback(callback)                         // Optional callback is MapViewPager.Callback
        .markersAlpha(alpha)                        // Optional
        .mapPadding(left, top, right, bottom)       // Optional
        .mapOffset(offset)                          // Optional
        .build();
```

Check the examples on the [sample folder](https://github.com/nitrico/mapviewpager/tree/master/sample).


## Author

##### Miguel Ángel Moreno

I'm available to be hired, Contact me!

|[Email](mailto:nitrico@gmail.com)|[Facebook](https://www.facebook.com/miguelangelmoreno)|[Google+](https://plus.google.com/+Miguel%C3%81ngelMorenoS)|[Linked.in](https://www.linkedin.com/in/morenomiguelangel)|[Twitter](https://twitter.com/nitrico/)
|---|---|---|---|---|


## License
```
Copyright 2016 Miguel Ángel Moreno

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
