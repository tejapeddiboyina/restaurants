<template>
  <div>
    <div v-for="restaurant in restaurants" :key="restaurant.RestaurantID" class="row" id="res">
      <div class="col-sm-8">
        <img :alt="restaurant.RestaurantName" :src="abc" style="width:200px;height:200px">
        <br>

        <label for>Restaurant Name:</label>
        <span>{{restaurant.RestaurantName}}</span>
        <br><br>

        <label for>Restaurant Cuisines:</label>
        <span>{{restaurant.Cuisines}}</span>
        <br><br>

        <label for>Restaurant Cost:</label>
        <span>{{restaurant.AverageCostForTwo}}</span>
        <br><br>

        <label for>Restaurant Rating:</label>
        <span>{{restaurant.RatingText}}</span>
        <br><br>

        <label for>Restaurant Votes:</label>
        <span>{{restaurant.Votes}}</span>
        <br>
      </div>
      <div class="col-sm-4">
        <showMap :restaurantID="restaurant.RestaurantID" />
      </div>
    </div>
  </div>
</template>




<script>
import showMap from './showMap';
export default {
  props: ["restaurants"],
  components: {
    showMap
  }
};
</script>




<style>
#res {
  margin: 10px;

  border: 6px solid grey;

  border-radius: 20px;

  padding: 10px;

  width: 100%;

  background-color: rgb(201, 139, 139);
}
</style>
