<template>
    <div ref="mapContainer" class="map-container"></div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import mapboxgl from 'mapbox-gl' // or "const mapboxgl = require('mapbox-gl');"
import 'mapbox-gl/dist/mapbox-gl.css'

mapboxgl.accessToken = 'pk.eyJ1IjoiZ2hjY3Jpc3RpYSIsImEiOiJjbDV5NWZqMDYwcTg3M2JtbTNuNWZnYmk5In0.q4ZXitWlCaKJPW-D--cl0Q'

const mapContainer = ref<HTMLElement>()

onMounted(() => {
    const map = new mapboxgl.Map({
        container: mapContainer.value!, // container ID
        style: 'mapbox://styles/mapbox/streets-v11', // style URL
        center: [-74.5, 40], // starting position [lng, lat]
        zoom: 2, // starting zoom
        projection: 'globe', // display the map as a 3D globe
    } as never)
    map.on('style.load', () => {
        map.setFog({
            // Set the default atmosphere style
            color: 'rgb(186, 210, 235)', // Lower atmosphere
            'high-color': 'rgb(36, 92, 223)', // Upper atmosphere
            'horizon-blend': 0.02, // Atmosphere thickness (default 0.2 at low zooms)
            'space-color': 'rgb(11, 11, 25)', // Background color
            'star-intensity': 0.6, // Background star brightness (default 0.35 at low zoooms )
        } as never)
    })
})
</script>

<style scoped>
.map-container {
    height: 100vh;
    width: 100vw;
}
</style>
