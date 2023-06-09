<!DOCTYPE html>
<html lang='en'>
  <head>
    <meta charset='utf-8' />
    <title>LGBTQ+ Businesses</title>
    <meta name='viewport' content='width=device-width, initial-scale=1' />
    <script src='https://api.tiles.mapbox.com/mapbox-gl-js/v2.14.1/mapbox-gl.js'></script>
    <link href='https://api.tiles.mapbox.com/mapbox-gl-js/v2.14.1/mapbox-gl.css' rel='stylesheet' />
    <style>
      body { 
        margin: 0; 
        padding: 0; 
      }
      #map { 
        position: absolute; 
        top: 0; 
        bottom: 0; 
        width: 100%; 
      }
    </style>
  </head>
  <body>
    <div id='map'></div>
    <script>
    // The value for 'accessToken' begins with 'pk...'
    mapboxgl.accessToken = 'pk.eyJ1Ijoia2VsbHliYXVlciIsImEiOiJjbGk0d3h5YnEwMnk2M3JyNGRpeXh1MW4xIn0.XLy3Mw9CoXXbJvehWwuI6w'; 
    const map = new mapboxgl.Map({
      container: 'map',
      // Replace YOUR_STYLE_URL with your style URL.
      style: 'mapbox://styles/kellybauer/cli4xi5u3034q01p697ba8brd', 
      center: [-87.648336, 41.876314],
      zoom: 10.94
    });

    /* 
Add an event listener that runs
  when a user clicks on the map element.
*/
map.on('click', (event) => {
  // If the user clicked on one of your markers, get its information.
  const features = map.queryRenderedFeatures(event.point, {
    layers: ['lgbtq-businesses'] // replace with your layer name
  });
  if (!features.length) {
    return;
  }
  const feature = features[0];

/* 
    Create a popup, specify its options 
    and properties, and add it to the map.
  */
const popup = new mapboxgl.Popup({ offset: [0, -15] })
  .setLngLat(feature.geometry.coordinates)
  .setHTML(
    `<h3>${feature.properties.Business}</h3><p>${feature.properties.Description}</p><p><b>Website:</b> ${feature.properties.Website}</p><p><b>Address:</b> ${feature.properties.Address}</p>`
  )
  .addTo(map);

  // Code from the next step will go here.
});

map.addControl(new mapboxgl.NavigationControl());

    </script>
  </body>
</html>
