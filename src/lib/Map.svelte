<script>
   import { onMount } from 'svelte';

   onMount(async () => {
      const leaflet = await import('leaflet');
      const L = leaflet.default ?? leaflet;
      await import('leaflet/dist/leaflet.css');

      const map = L.map('map').setView([0,0], 2);

      L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
         maxZoom: 19,
         attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>'
      }).addTo(map);

      return () => map.remove();
   });
</script>

<div id="map" class="m-5" style="height: 600px;"></div>