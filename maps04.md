# Mapsの装飾

##　線を引く

```java
    private void setUpMap() {

        mMap.addMarker(new MarkerOptions().position(new LatLng(0, 0)).title("Marker"));

        LatLng startPos = new LatLng(36.550796, 139.929061);
        LatLng endPos = new LatLng(36.560147, 139.898935);

        mMap.addPolyline(new PolylineOptions()
                .add(startPos, endPos)
                .width(40)
                .color(Color.BLUE));

        mMap.moveCamera(CameraUpdateFactory.newLatLng(startPos));
        mMap.animateCamera(CameraUpdateFactory.zoomTo(13));
        
    }
```