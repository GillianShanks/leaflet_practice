<template lang="html">
  <div id="mapid">
    <l-map ref="myMap" :minZoom="minZoom" :maxZoom="maxZoom" :crs="crs">

      <l-image-overlay :url="url" :bounds="bounds"/>

      <l-marker v-for="planet in planets" :lat-lng="plant" :key="planet.name">
        <l-popup :content="planet.name" />
      </l-marker>

    </l-map>
</div>
</template>

<script>
import {CRS} from 'leaflet';
import {LMap, LImageOverlay, LMarker, LPopup} from 'vue2-leaflet';

export default {
  name: "leaflet-map",
  components: {
    LMap,
    LImageOverlay,
    LMarker,
    LPopup
  },
  data(){
    return {
      url: "http://localhost:8080/img/solar-system.207dccd8.jpg",
      bounds:[[0, 0], [100, 100]],
      minZoom: 0,
      maxZoom: 0,
      crs: CRS.Simple,
      planets:[
        {name: "Sun", lng: 0, lat:0}
        // {name: "Mercury", lng: 41.6, lat: 130.1 }
      ]
    }
  },
  mounted () {
      this.$refs.myMap.mapObject.setView([0,0], 0);
  }
}
</script>

<style lang="css" scoped>
/* @import "../node_modules/leaflet/dist/leaflet.css"; */

/* .leaflet-fake-icon-image-2x {
  background-image: url('../node_modules/leaflet/dist/images/marker-icon-2x.png');
}
.leaflet-fake-icon-shadow {
  background-image: url('../node_modules/leaflet/dist/images/marker-shadow.png');
} */

#mapid {
  height: 50vh;
  width: 90vw;
}
</style>
