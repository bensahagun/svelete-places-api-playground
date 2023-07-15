<script>
    import { onMount } from 'svelte';
  
    let coffeeShops = [];
  
    onMount(() => {
      const latitude = 14.337020 ; // Example latitude
      const longitude = 121.064365; // Example longitude
      const radius = 5000; // Search radius in meters
  
      const mapOptions = {
        center: { lat: latitude, lng: longitude },
        zoom: 15,
      };
  
      const map = new google.maps.Map(document.getElementById('map'), mapOptions);
  
      const request = {
        location: { lat: latitude, lng: longitude },
        radius: radius,
        type: 'cafe',
      };
  
      const service = new google.maps.places.PlacesService(map);
      service.nearbySearch(request, (results, status) => {
        if (status === google.maps.places.PlacesServiceStatus.OK) {
          coffeeShops = results;
        }
      });
    });
  </script>
  
  <main>
    <h1>Nearby Cafe</h1>
    <div id="map" style="height: 400px;"></div>
  
    {#if coffeeShops.length > 0}
      <ul>
        {#each coffeeShops as coffeeShop}
          <li>{coffeeShop.name}</li>
        {/each}
      </ul>
    {:else}
      <p>No coffee shops found nearby.</p>
    {/if}
  </main>
  