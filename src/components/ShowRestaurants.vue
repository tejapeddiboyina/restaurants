<template>
  <div class="row">
    <div v-for="restaurant in restaurants" :key="restaurant.RestaurantID" class="col-sm-4" id="res">
      <img :alt="restaurant.RestaurantName" :src="abc" style="width:200px;height:200px">
      <br>

      <label for>Restaurant Name:</label>
      <span>{{restaurant.RestaurantName}}</span>
      <br>

      <label for>Restaurant Cuisines:</label>
      <span>{{restaurant.Cuisines}}</span>
      <br>

      <label for>Restaurant Cost:</label>
      <span>{{restaurant.AverageCostForTwo}}</span>
      <br>

      <label for>Restaurant Rating:</label>
      <span>{{restaurant.RatingText}}</span>
      <br>

      <label for>Restaurant Votes:</label>
      <span>{{restaurant.Votes}}</span>
      <br>
    </div>
  </div>
</template>




<script>
export default {
  props: ["restaurants"]
};
</script>




<style>
#res {
  margin: 20px;

  border: 6px solid grey;

  border-radius: 20px;

  padding: 10px;

  width: 250px;

  height: 250px;

  float: left;

  background-color: rgb(201, 139, 139);
}
</style>
