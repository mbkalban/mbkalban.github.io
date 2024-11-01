<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Return-as-You-Receive Service Demo</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      text-align: center;
      margin-top: 20px;
    }
    #return-button, #open-map-button, #distance-button {
      background-color: #ff6a00;
      color: white;
      padding: 15px 30px;
      border: none;
      border-radius: 5px;
      font-size: 16px;
      cursor: pointer;
      margin: 10px;
    }
    #map-container {
      display: none;
      margin-top: 20px;
    }
    #map {
      width: 100%;
      height: 300px;
      border: 1px solid #ddd;
      border-radius: 8px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
    }
  </style>
</head>
<body>

<h2>Return-as-You-Receive Service</h2>
<p>Click the button below to initiate your return and notify a nearby driver.</p>

<!-- Initial Return Button -->
<button id="return-button" onclick="notifyDriver()">Return Now</button>

<!-- Open Map Button (Hidden initially) -->
<button id="open-map-button" onclick="showMap()" style="display:none;">Open Map</button>

<!-- Map Container -->
<div id="map-container">
  <p>A driver is nearby and will pick up your item shortly!</p>
  <iframe src="https://www.google.com/maps/embed?pb=!1m14!1m12!1m3!1d758.292280648802!2d55.50511570616299!3d25.30197639283665!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!5e0!3m2!1sen!2sae!4v1730460256833!5m2!1sen!2sae" width="600" height="450" style="border:0;" allowfullscreen="" loading="lazy" referrerpolicy="no-referrer-when-downgrade"></iframe>
  
  <!-- Calculate Distance Button -->
  <button id="distance-button" onclick="calculateDistance()">Calculate Distance</button>
</div>

<script>
  function notifyDriver() {
    // Show notification message
    alert("A driver is nearby and has been notified to pick up your item for return!");
    
    // Display the "Open Map" button
    document.getElementById('open-map-button').style.display = 'inline-block';
  }

  function showMap() {
    // Display the map container
    document.getElementById('map-container').style.display = 'block';
  }

  function calculateDistance() {
    // Coordinates for a sample driver location and user location
    const driverLocation = { lat: 25.301976, lng: 55.505115 };
    const userLocation = { lat: 25.310181159590925, lng: 55.493398657183704 };

    // Calculate the distance (mock example)
    const distance = getDistanceFromLatLonInKm(driverLocation.lat, driverLocation.lng, userLocation.lat, userLocation.lng);
    
    alert(`The driver is approximately ${distance.toFixed(2)} km away from you!`);
  }

  // Haversine formula to calculate the distance between two coordinates
  function getDistanceFromLatLonInKm(lat1, lon1, lat2, lon2) {
    const R = 6371; // Radius of the Earth in km
    const dLat = deg2rad(lat2 - lat1);
    const dLon = deg2rad(lon2 - lon1); 
    const a = 
      Math.sin(dLat/2) * Math.sin(dLat/2) +
      Math.cos(deg2rad(lat1)) * Math.cos(deg2rad(lat2)) * 
      Math.sin(dLon/2) * Math.sin(dLon/2)
      ; 
    const c = 2 * Math.atan2(Math.sqrt(a), Math.sqrt(1-a)); 
    return R * c; // Distance in km
  }

  function deg2rad(deg) {
    return deg * (Math.PI/180);
  }
</script>

</body>
</html>
