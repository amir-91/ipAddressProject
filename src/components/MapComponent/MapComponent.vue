<template>
  <GoogleMap
    class="IpSearch__map"
    api-key="AIzaSyDYdBtTkh9NUqIRd1XIOznpGxUHahTNT1o"
    style="height: 100%"
    :center="center"
    :zoom="15"
    :options="{zoomControl: false}"
  >
    <CustomMarker :options="{ position: center}">
      <div style="text-align: center">
        <img src="../../assets/images/marker.png" width="50" height="50"/>
      </div>
    </CustomMarker>
  </GoogleMap>
</template>

<script>
import { GoogleMap, CustomMarker } from "vue3-google-map";
export default {
  props: ["center"],
  components: {
    GoogleMap,
    CustomMarker
  }
};
</script>
