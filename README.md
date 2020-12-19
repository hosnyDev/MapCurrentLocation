# MapCurrentLocation

###### 1.dependencies
```
    // map
    implementation 'com.google.android.gms:play-services-maps:17.0.0'
    implementation 'com.google.android.gms:play-services-places:17.0.0'
    implementation 'com.google.android.libraries.places:places:2.4.0'


```
###### 2.manifest
```
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />

    <uses-feature
        android:name="android.hardware.location.gps"
        android:required="true" />
    
    <meta-data
        android:name="com.google.android.geo.API_KEY"
        android:value="@string/google_maps_key" />

    <uses-library
        android:name="org.apache.http.legacy"
        android:required="false" />

```

###### 3.layout.activity_maps
```
    <?xml version="1.0" encoding="utf-8"?>
    <RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        xmlns:tools="http://schemas.android.com/tools"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        android:orientation="vertical"
        tools:context=".MapsActivity">

        <com.google.android.material.appbar.AppBarLayout
            android:id="@+id/AppBarLayout"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:background="@color/white"
            android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar">

            <androidx.appcompat.widget.Toolbar
                android:id="@+id/toolbar"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:background="@color/white"
                android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar"
                app:layout_scrollFlags="scroll|enterAlways"
                app:navigationIcon="@drawable/ic_back"
                app:popupTheme="@style/ThemeOverlay.AppCompat.Light">

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="40dp">

                    <TextView
                        android:layout_width="0dp"
                        android:layout_height="wrap_content"
                        android:layout_gravity="center_vertical"
                        android:layout_weight="1"
                        android:text="@string/set_location_on_map"
                        android:textColor="@color/black"
                        android:textSize="18sp"
                        android:textStyle="bold" />

                </LinearLayout>
            </androidx.appcompat.widget.Toolbar>


        </com.google.android.material.appbar.AppBarLayout>

        <fragment
            android:id="@+id/map"
            android:name="com.google.android.gms.maps.SupportMapFragment"
            android:layout_width="match_parent"
            android:layout_height="match_parent"
            android:layout_below="@id/AppBarLayout" />

        <!-- search bar layout -->
        <include
            android:id="@+id/search_bar"
            layout="@layout/include_card_view_search_bar_map"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_below="@id/AppBarLayout" />


        <androidx.cardview.widget.CardView
            android:id="@+id/card"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_alignParentBottom="true"
            android:layout_gravity="center_horizontal"
            android:layout_margin="8dp"
            app:cardBackgroundColor="@color/card_bg"
            app:cardCornerRadius="25dp"
            app:cardElevation="5dp">

            <LinearLayout
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                android:orientation="horizontal">

                <ProgressBar
                    android:id="@+id/progressChangMap"
                    android:layout_width="34dp"
                    android:layout_height="34dp"
                    android:layout_gravity="center_vertical"
                    android:layout_marginStart="16dp"
                    android:padding="8dp" />

                <Button
                    android:id="@+id/btnSetMap"
                    android:layout_width="0dp"
                    android:layout_height="wrap_content"
                    android:layout_weight="1"
                    android:background="@null"
                    android:textAllCaps="false"
                    android:textColor="@color/white" />

                <ProgressBar
                    android:layout_width="34dp"
                    android:layout_height="34dp"
                    android:layout_marginEnd="16dp"
                    android:padding="8dp"
                    android:visibility="invisible" />

            </LinearLayout>

        </androidx.cardview.widget.CardView>

        <ImageView
            android:layout_width="50dp"
            android:layout_height="50dp"
            android:layout_centerHorizontal="true"
            android:layout_centerVertical="true"
            android:contentDescription="@string/todo"
            android:src="@drawable/ic_location" />

        <com.google.android.material.floatingactionbutton.FloatingActionButton
            android:id="@+id/fab_directions"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_above="@id/card"
            android:layout_alignParentEnd="true"
            android:layout_margin="18dp"
            android:layout_marginTop="50dp"
            android:clickable="true"
            android:focusable="true"
            android:src="@drawable/ic_current_location"
            app:backgroundTint="@color/white"
            app:fabSize="normal" />

    </RelativeLayout>

```

###### 4.layout/include_card_view_search_bar_map
```
  <?xml version="1.0" encoding="utf-8"?>
  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
      xmlns:app="http://schemas.android.com/apk/res-auto"
      android:id="@+id/search"
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:fitsSystemWindows="true"
      android:orientation="vertical">

      <androidx.cardview.widget.CardView
          android:id="@+id/search_bar"
          android:layout_width="match_parent"
          android:layout_height="wrap_content"
          android:layout_margin="8dp"
          android:padding="4dp"
          app:cardBackgroundColor="@android:color/white"
          app:cardCornerRadius="10dp"
          app:cardElevation="3dp">

          <LinearLayout
              android:layout_width="match_parent"
              android:layout_height="wrap_content"
              android:baselineAligned="false"
              android:orientation="horizontal">

              <fragment
                  android:id="@+id/place_autocomplete_fragment"
                  android:name="com.google.android.libraries.places.widget.AutocompleteSupportFragment"
                  android:layout_width="0dp"
                  android:layout_height="50dp"
                  android:layout_gravity="center_vertical"
                  android:layout_weight="1" />

          </LinearLayout>

      </androidx.cardview.widget.CardView>


  </LinearLayout>

  ```


###### 5.MapsActivity

```
  import android.Manifest;
  import android.content.Context;
  import android.content.Intent;
  import android.content.pm.PackageManager;
  import android.location.Address;
  import android.location.Geocoder;
  import android.location.Location;
  import android.location.LocationListener;
  import android.location.LocationManager;
  import android.net.Uri;
  import android.os.Build;
  import android.os.Bundle;
  import android.provider.Settings;
  import android.view.View;
  import android.widget.Button;
  import android.widget.ProgressBar;
  import android.widget.Toast;

  import androidx.appcompat.app.AlertDialog;
  import androidx.appcompat.widget.Toolbar;
  import androidx.cardview.widget.CardView;
  import androidx.core.app.ActivityCompat;
  import androidx.core.content.ContextCompat;
  import androidx.fragment.app.FragmentActivity;

  import com.google.android.gms.common.api.Status;
  import com.google.android.gms.maps.CameraUpdateFactory;
  import com.google.android.gms.maps.GoogleMap;
  import com.google.android.gms.maps.SupportMapFragment;
  import com.google.android.gms.maps.model.BitmapDescriptorFactory;
  import com.google.android.gms.maps.model.LatLng;
  import com.google.android.gms.maps.model.Marker;
  import com.google.android.gms.maps.model.MarkerOptions;
  import com.google.android.libraries.places.api.Places;
  import com.google.android.libraries.places.api.model.Place;
  import com.google.android.libraries.places.widget.AutocompleteSupportFragment;
  import com.google.android.libraries.places.widget.listener.PlaceSelectionListener;

  import java.io.IOException;
  import java.util.Arrays;
  import java.util.List;
  import java.util.Locale;

  public class MapsActivity extends FragmentActivity {

      // view
      private GoogleMap mMap;
      private ProgressBar progressBar;
      private Button btnSetMap;
      private CardView card;

      // current location
      private LocationManager mLocationManager;
      public static final int LOCATION_UPDATE_MIN_DISTANCE = 1;
      public static final int LOCATION_UPDATE_MIN_TIME = 1000;
      private Marker marker;

      @Override
      protected void onCreate(Bundle savedInstanceState) {
          super.onCreate(savedInstanceState);
          setContentView(R.layout.activity_maps);

          // toolbar
          Toolbar toolbar = findViewById(R.id.toolbar);
          toolbar.setNavigationOnClickListener(v -> finish());

          // findView
          progressBar = findViewById(R.id.progressChangMap);
          btnSetMap = findViewById(R.id.btnSetMap);
          card = findViewById(R.id.card);

          initMapFragment();
          mLocationManager = (LocationManager) getSystemService(Context.LOCATION_SERVICE);


          // get selected position
          btnSetMap.setOnClickListener(v -> {

              if (mMap != null) {
                  saveLatLong(mMap.getCameraPosition().target.latitude, mMap.getCameraPosition().target.longitude);
                  finish();
              } else
                  Toast.makeText(this, R.string.Pleaseselectlocation, Toast.LENGTH_SHORT).show();

          });

          // update current location
          findViewById(R.id.fab_directions).setOnClickListener(v -> {
              try {
                  getCurrentLocation();
                  //mMap.animateCamera(zoomingLocation());
              } catch (Exception e) {
                  Toast.makeText(this, e.getMessage(), Toast.LENGTH_SHORT).show();
              }
          });


          // Initialize the SDK
          if (!Places.isInitialized()) {
              Places.initialize(getApplicationContext(), getString(R.string.google_maps_key));
          }

          // Initialize the AutocompleteSupportFragment.
          AutocompleteSupportFragment autocompleteFragment = (AutocompleteSupportFragment)
                  getSupportFragmentManager().findFragmentById(R.id.place_autocomplete_fragment);

          if (autocompleteFragment != null) {
              autocompleteFragment.setPlaceFields(Arrays.asList(Place.Field.ID, Place.Field.NAME));

              autocompleteFragment.setOnPlaceSelectedListener(new PlaceSelectionListener() {
                  @Override
                  public void onPlaceSelected(Place place) {

                    // TODO: Get info about the selected place.
                      //  Log.i(TAG, "Place: " + place.getName() + ", " + place.getId());

                      marker = mMap.addMarker(new MarkerOptions()
                              .position(place.getLatLng())
                              .title("Place: " + place.getName() + ", " + place.getId())
                              .icon(BitmapDescriptorFactory.fromResource(R.drawable.null_image)));


                      marker.showInfoWindow();

                      mMap.animateCamera(CameraUpdateFactory.newLatLngZoom(place.getLatLng(), 15));

                  }

                  @Override
                  public void onError(Status status) {
                 new AlertDialog.Builder(MapsActivity.this)
                            .setMessage("An error occurred: \n" + status)
                            .setNegativeButton("ok", null)
                            .create()
                            .show();
                  }
              });
          }
      }

      @Override
      protected void onStart() {
          super.onStart();
          getCurrentLocation();
      }


      private void initMapFragment() {
          SupportMapFragment mapFragment = (SupportMapFragment) getSupportFragmentManager().findFragmentById(R.id.map);
          mapFragment.getMapAsync(googleMap -> {
              // set map type
              googleMap.setMapType(GoogleMap.MAP_TYPE_NORMAL);
              // Enable / Disable zooming controls
              googleMap.getUiSettings().setZoomControlsEnabled(false);

              // Enable / Disable Compass icon
              googleMap.getUiSettings().setCompassEnabled(true);
              // Enable / Disable Rotate gesture
              googleMap.getUiSettings().setRotateGesturesEnabled(true);
              // Enable / Disable zooming functionality
              googleMap.getUiSettings().setZoomGesturesEnabled(true);

              googleMap.getUiSettings().setScrollGesturesEnabled(true);
              googleMap.getUiSettings().setMapToolbarEnabled(true);

              // set zoom in first marker
              // googleMap.moveCamera(CameraUpdateFactory.newLatLngZoom(latLng, 1));

              mMap = googleMap;

              mMap.setOnMapClickListener(latLng -> {

                  marker = mMap.addMarker(new MarkerOptions()
                          .position(latLng)
                          .icon(BitmapDescriptorFactory.fromResource(R.drawable.null_image)));
                  marker.showInfoWindow();

                  mMap.animateCamera(CameraUpdateFactory.newLatLngZoom(latLng, 15));

                  saveLatLong(latLng.latitude, latLng.longitude);

              });

              mMap.setOnCameraIdleListener(() -> {
                  progressBar.setVisibility(View.VISIBLE);
                  btnSetMap.setText(R.string.Working);
                  LatLng position = mMap.getCameraPosition().target;
                  progressBar.setVisibility(View.GONE);
                  card.setCardBackgroundColor(getResources().getColor(R.color.card_bg));
                  btnSetMap.setTextColor(getResources().getColor(R.color.white));
                  btnSetMap.setText(R.string.SetthisLocation);

                  saveLatLong(position.latitude, position.longitude);
              });

              mMap.setOnCameraMoveStartedListener(i -> {
                  progressBar.setVisibility(View.VISIBLE);
                  card.setCardBackgroundColor(getResources().getColor(R.color.white));
                  btnSetMap.setTextColor(getResources().getColor(R.color.card_bg));
                  btnSetMap.setText(R.string.Working);
              });


          });
      }

      private void saveLatLong(double latitude, double longitude) {
          getSharedPreferences("locationShop", MODE_PRIVATE)
                  .edit()
                  .putString("lat", String.valueOf(latitude))
                  .putString("long", String.valueOf(longitude))
                  .apply();
      }

      private void getCurrentLocation() {

          boolean isGPSEnabled = mLocationManager.isProviderEnabled(LocationManager.GPS_PROVIDER);
          boolean isNetworkEnabled = mLocationManager.isProviderEnabled(LocationManager.NETWORK_PROVIDER);

          Location location = null;
          if (!(isGPSEnabled || isNetworkEnabled))
              //turnGPSOn();
              buildAlertMessageNoGps();
          else {
              if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.M) {
                  if (ContextCompat.checkSelfPermission(this, Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
                      ActivityCompat.requestPermissions(this, new String[]{Manifest.permission.ACCESS_FINE_LOCATION}, 1);
                  } else {

                      if (isNetworkEnabled) {
                          mLocationManager.requestLocationUpdates(LocationManager.NETWORK_PROVIDER,
                                  LOCATION_UPDATE_MIN_TIME, LOCATION_UPDATE_MIN_DISTANCE, mLocationListener);
                          location = mLocationManager.getLastKnownLocation(LocationManager.NETWORK_PROVIDER);
                      }

                      if (isGPSEnabled) {
                          mLocationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER,
                                  LOCATION_UPDATE_MIN_TIME, LOCATION_UPDATE_MIN_DISTANCE, mLocationListener);
                          location = mLocationManager.getLastKnownLocation(LocationManager.GPS_PROVIDER);
                      }
                  }
              } else {

                  if (isNetworkEnabled) {
                      mLocationManager.requestLocationUpdates(LocationManager.NETWORK_PROVIDER,
                              LOCATION_UPDATE_MIN_TIME, LOCATION_UPDATE_MIN_DISTANCE, mLocationListener);
                      location = mLocationManager.getLastKnownLocation(LocationManager.NETWORK_PROVIDER);
                  }

                  if (isGPSEnabled) {
                      mLocationManager.requestLocationUpdates(LocationManager.GPS_PROVIDER,
                              LOCATION_UPDATE_MIN_TIME, LOCATION_UPDATE_MIN_DISTANCE, mLocationListener);
                      location = mLocationManager.getLastKnownLocation(LocationManager.GPS_PROVIDER);
                  }
              }


          }
          if (location != null) {

              drawMarker(location);
          }
      }

      private void drawMarker(Location location) {

          if (mMap != null) {

              if (marker != null)
                  marker.remove();

              LatLng gps = new LatLng(location.getLatitude(), location.getLongitude());

              marker = mMap.addMarker(new MarkerOptions()
                      .position(gps)
                      .title(getString(R.string.YourLocation))
                      .icon(BitmapDescriptorFactory.fromResource(R.drawable.null_image)));

              marker.showInfoWindow();

              mMap.animateCamera(CameraUpdateFactory.newLatLngZoom(gps, 15));

              saveLatLong(gps.latitude, gps.longitude);
          }
      }

      private LocationListener mLocationListener = new LocationListener() {
          @Override
          public void onLocationChanged(Location location) {
              if (location != null) {
                  //  Logger.d(String.format("%f, %f", location.getLatitude(), location.getLongitude()));
                  drawMarker(location);
                  mLocationManager.removeUpdates(mLocationListener);
              } else {
                  //Logger.d("Location is null");
                  Toast.makeText(MapsActivity.this, R.string.Locationisnull, Toast.LENGTH_SHORT).show();
              }
          }

          @Override
          public void onStatusChanged(String s, int i, Bundle bundle) {

          }

          @Override
          public void onProviderEnabled(String s) {

          }

          @Override
          public void onProviderDisabled(String s) {

          }
      };

      private void buildAlertMessageNoGps() {
          final AlertDialog.Builder builder = new AlertDialog.Builder(this);
          builder.setMessage(getString(R.string.enablegps))
                  .setCancelable(false)
                  .setPositiveButton(getString(R.string.yes), (dialog, id) -> startActivity(new Intent(Settings.ACTION_LOCATION_SOURCE_SETTINGS)))
                  .setNegativeButton(getString(R.string.no), (dialog, id) -> dialog.cancel());
          final AlertDialog alert = builder.create();
          alert.show();
      }

      public String getAddress(Context context, double lat, double lng) {
          Geocoder geocoder = new Geocoder(context, Locale.getDefault());
          try {
              List<Address> addresses = geocoder.getFromLocation(lat, lng, 1);
              Address obj = addresses.get(0);

              String add = obj.getAddressLine(0);
              add = add + "\n" + obj.getCountryName();
              add = add + "\n" + obj.getCountryCode();
              add = add + "\n" + obj.getAdminArea();
              add = add + "\n" + obj.getPostalCode();
              add = add + "\n" + obj.getSubAdminArea();
              add = add + "\n" + obj.getLocality();
              add = add + "\n" + obj.getSubThoroughfare();

              return add;
          } catch (IOException e) {
              e.printStackTrace();
              Toast.makeText(this, e.getMessage(), Toast.LENGTH_SHORT).show();
              return null;
          }
      }

      private void turnGPSOn() {
          String provider = Settings.Secure.getString(getContentResolver(), Settings.Secure.LOCATION_PROVIDERS_ALLOWED);

          if (!provider.contains("gps")) { //if gps is disabled
              final Intent poke = new Intent();
              poke.setClassName("com.android.settings", "com.android.settings.widget.SettingsAppWidgetProvider");
              poke.addCategory(Intent.CATEGORY_ALTERNATIVE);
              poke.setData(Uri.parse("3"));
              sendBroadcast(poke);
          }
      }

  }


```
