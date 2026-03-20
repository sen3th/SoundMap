<script>
   import { onMount } from 'svelte';
    import CountryCard from '$lib/CountryCard.svelte';


    // country finder

   let selectedCountry = $state('');
    let marker;


    //map setup

    onMount(async () => {
      const leaflet = await import('leaflet');
      const L = leaflet.default ?? leaflet;
      await import('leaflet/dist/leaflet.css');

      const map = L.map('map').setView([0,0], 2);
      map.setMaxBounds([[-90, -180], [90, 180]]);

      L.tileLayer('https://tile.openstreetmap.org/{z}/{x}/{y}.png', {
         maxZoom: 19,
         attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a>'
      }).addTo(map);


      // country finder
        map.on('click', async (e) => {
            const latitude = e.latlng.lat;
            const longitude = e.latlng.lng;

            selectedCountry = 'Loading...';

         try {
            const url = `https://api.bigdatacloud.net/data/reverse-geocode-client?latitude=${latitude}&longitude=${longitude}&localityLanguage=en`;

            const res = await fetch(url);
            const data = await res.json();
            selectedCountry = data.countryName || 'Country not found';

            if (marker) marker.remove();
            marker = L.marker([latitude, longitude]).addTo(map);
            } catch {
            selectedCountry = 'Error fetching country';
         }
        });


        return () => map.remove();
   });
</script>

<div class="m-5 flex flex-col gap-5 lg:flex-row lg:items-start">
   <div id="map" class="w-full lg:w-2/3" style="height: 400px;"></div>

   <div class="w-full lg:w-1/3">
      <CountryCard country={selectedCountry}/>
   </div>
</div>

