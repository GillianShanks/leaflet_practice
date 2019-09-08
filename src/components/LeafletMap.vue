<template lang="html">
  <div id="mapid">
    <l-map @click="handleMapClick" ref="myMap" :minZoom="minZoom" :maxZoom="maxZoom" :crs="crs">

      <l-image-overlay :url="url" :bounds="bounds"/>

      <l-marker v-for="planet in planets" :lat-lng="planet" :key="planet.name">
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
      bounds:[[-400, 0], [0, 1100]],
      minZoom: -10,
      maxZoom: 4,
      crs: CRS.Simple,
      planets:[
        {name: "Sun", lat:-200, lng: 35},
        {name: "Mercury", lat:-200, lng: 125},
        {name: "Venus", lat:-200, lng: 185},
        {name: "Earth", lat:-200, lng: 265},
        {name: "Mars", lat:-200, lng: 350},
        {name: "Jupiter", lat:-200, lng: 500},
        {name: "Saturn", lat:-200, lng: 680},
        {name: "Uranus", lat:-200, lng: 860},
        {name: "Neptune", lat:-200, lng: 990},
      ],
      mapx: null,
      mapy: null
    }
  },
  mounted () {
      // this.$refs.myMap.mapObject.setView([0,0], 0);
      this.$refs.myMap.mapObject.fitBounds(this.bounds);
  },
  methods:{
    handleMapClick(e){
      let x=e.containerPoint.x
      let y=e.containerPoint.y

      let imageWidth =1280
      let imageHeight =426

      let mapHeight = this.$refs.myMap.mapObject._container.offsetHeight
      let mapWidth = this.$refs.myMap.mapObject._container.offsetWidth

      this.mapx =x * imageWidth/mapWidth;
      this.mapy =y * imageHeight/mapHeight;

      console.log(x, y);
    }
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
  height: 400px;
  width: 1100px;
}
</style>
