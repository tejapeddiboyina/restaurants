<template>
  <div ref="map" style="width:280px; height: 300px"></div>
</template>



<script>
export default {
  props: ["restaurantID"],

  data() {
    return {
      platform: {},

      app_id: "wbUwTytf7TbXAzXPKqlr",

      app_code: "tZXakDM_YNmoZ4NKD_kguQ",

      lnglat: {},

      restaurant_address: require("../data/restaurant_places.json")
    };
  },

  created() {
    this.platform = new H.service.Platform({
      app_id: this.app_id,

      app_code: this.app_code
    });
  },

  mounted() {
    for (var restaurant of this.restaurant_address) {
      if (restaurant.RestaurantID == this.restaurantID) {
        this.lnglat = {
          lng: restaurant.Longitude,
          lat: restaurant.Latitude
        };

        break;
      }
    }

    var map = new H.Map(
      this.$refs.map,

      this.platform.createDefaultLayers().normal.map,

      {
        zoom: 13,

        center: this.lnglat,

        gestureHandling: "cooperative"
      }
    );

    map.addObject(new H.map.Marker(this.lnglat));

    var behavior = new H.mapevents.Behavior(new H.mapevents.MapEvents(map));

    var ui = H.ui.UI.createDefault(map, this.platform.createDefaultLayers());
  }
};
</script>
