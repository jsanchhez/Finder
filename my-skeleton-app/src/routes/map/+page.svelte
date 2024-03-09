<script>
    import { onMount } from 'svelte';
    import L from 'leaflet';
    import 'leaflet/dist/leaflet.css';
    


  
    /**
	 * @type {{ setView: (arg0: number[], arg1: number) => void; }}
	 */
    let map;
  
    onMount(() => {
      map = L.map('map').setView([51.505, -0.09], 13);
  
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '© OpenStreetMap contributors'
      }).addTo(map);
  
      navigator.geolocation.getCurrentPosition((position) => {
        const { latitude, longitude } = position.coords;
        L.marker([latitude, longitude]).addTo(map)
          .bindPopup('You are here!')
          .openPopup();
  
        map.setView([latitude, longitude], 13);
      });
    });
    const leafletScript = document.createElement('script');
  leafletScript.src = 'https://unpkg.com/leaflet@1.9.4/dist/leaflet.js';
  leafletScript.integrity = 'sha256-20nQCchB9co0qIjJZRGuk2/Z9VM+kNiyxNV1lvTlZBo=';
  leafletScript.crossOrigin = '';
  document.head.appendChild(leafletScript);
  </script>
  
  <style>
    @import 'https://unpkg.com/leaflet@1.9.4/dist/leaflet.css';
    #map { height: 100vh; }
  </style>
  
  <div id="map"></div>