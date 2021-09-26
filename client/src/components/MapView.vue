<template>
  <div class="map">
    <GoogleMap
      api-key="AIzaSyBRwdrH1_YquIsowD6GNsIbLOTdbRczn3U"
      style="width: 100%; height: 100%"
      :center="center"
      :zoom="5"
    >
      <Polygon :options="bermudaTriangle" />
    </GoogleMap>
  </div>
</template>

<script>
import { defineComponent } from "vue";
import { GoogleMap, Polygon } from "vue3-google-map";

export default defineComponent({
  components: { GoogleMap, Polygon },
  setup() {
    const center = { lat: 24.886, lng: -70.268 };
    const triangleCoords = [
      { lat: 25.774, lng: -80.19 },
      { lat: 18.466, lng: -66.118 },
      { lat: 32.321, lng: -64.757 },
      { lat: 25.774, lng: -80.19 },
    ];
    const bermudaTriangle = {
      paths: triangleCoords,
      strokeColor: "#FF0000",
      strokeOpacity: 0.8,
      strokeWeight: 2,
      fillColor: "#FF0000",
      fillOpacity: 0.35,
    };

    return { center, bermudaTriangle };
  },
});
</script>

<style lang="scss" scoped>
.map {
  width: 100%;
  height: 25rem;
  margin: 5rem 0rem;
  border-radius: 1rem;
  border-radius: 1rem;
  overflow: hidden;
}
</style>