<!--<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  components: {
    HelloWorld
  }
}
</script>-->

<template>
  <div id="restaurants">
    <div class="container">
      <div class="row">
        <div class="col-sm-12 col-xs-12">
          <div v-on:keyup.enter="getRestaurantForTheCuisine" @click="resetsc">
            <label>Search for Cuisines:</label>
            <input type="text" placeholder="enter any cuisines" v-model="cuisine">
            <br>

            <p class="alert alert-warning" v-if="noCuisine">You are searching for none</p>
            <br>
          </div>
          <showCuisines v-if="showCuisine" :cuisine="cuisine" @replaceCuisine="changeCuisine"/>
        </div>
        <div class="col-sm-12 col-xs-12" @click="() => showCuisine = false">
          <p style="color:blue">or select cuisine from checkbox</p>
          <br>

          <div class="col-sm-12 col-xs-12">
            <span>order by {{selected}}</span>
            <br>

            <select v-model="selected">
              <option disabled value=" ">Please select one</option>

              <option>Cost</option>

              <option>Rating</option>

              <option>Votes</option>
            </select>

            <select v-model="AscDsc">
              <option>ASC</option>

              <option>DSC</option>
            </select>
          </div>
        </div>
      </div>

      <br>

      <div class="row">
        <p style="color:blue">{{numOfCuisineRest}} Restaurants are found</p>
      </div>
      <div class="row">
        <div id="sc" @click="resetcu" class="col-sm-3">
          <div v-for="cuis in Cuisines" :key="cuis">
            <input type="checkbox" :value="cuis" v-model="selectedCuisine" style="float: left">
            <span style="float:left">{{cuis}}</span>
            <br>
          </div>
        </div>

        <div class="col-sm-9 col-xs-12">
          <ShowRestaurants :restaurants="restaurantForTheCuisine"/>
        </div>
      </div>
    </div>
  </div>
</template>




<script>
import ShowRestaurants from "@/components/ShowRestaurants";
import showCuisines from "@/components/showCuisines";

export default {
  components: {
    ShowRestaurants,
    showCuisines
  },

  data() {
    return {
      restaurants: require("../data/restaurant_details.json"),

      cuisine: "",

      restaurantForTheCuisine: require("../data/restaurant_details.json"),

      noCuisine: false,

      Cuisines: require("../data/Cuisines"),

      selectedCuisine: [],

      s: new Set(),

      selected: "",

      AscDsc: "",

      showCuisine: false
    };
  },

  methods: {
    getRestaurantForTheCuisine() {
      if (this.cuisine) {
        this.noCuisine = false;
      } else {
        this.noCuisine = true;
      }
    },

    changeCuisine(val) {
      this.cuisine = val;
      this.showCuisine = false;
    },

    resetsc() {
      this.selectedCuisine = [];
      this.showCuisine = true;
      this.cuisine = "";
    },

    resetcu() {
      this.cuisine = "";
    }
  },

  computed: {
    numOfCuisineRest() {
      return this.restaurantForTheCuisine.length;
    },

    numOfCuis() {
      return this.selectedCuisine.length;
    }
  },

  watch: {
    cuisine: function() {
      this.noCuisine = false;

      this.restaurantForTheCuisine = [];

      this.restaurants.forEach(restaurant => {
        if (
          restaurant.Cuisines.toUpperCase().includes(this.cuisine.toUpperCase())
        ) {
          console.log(restaurant.Cuisines);

          this.restaurantForTheCuisine.push(restaurant);
        }
      });

      this.selected = "";
    },

    selectedCuisine: function(val) {
      this.restaurantForTheCuisine = [];

      this.s = new Set();

      val.forEach(value => {
        console.log();

        this.restaurants.forEach(restaurant => {
          if (restaurant.Cuisines.toUpperCase().includes(value.toUpperCase())) {
            console.log(restaurant.Cuisines);

            this.s.add(restaurant);
          }
        });
      });

      this.s.forEach(v => this.restaurantForTheCuisine.push(v));

      this.temp = this.selected;

      this.selected = "";
    },

    selected: {
      handler(val, oldVal) {
        if (val == "") {
          this.selected = oldVal;
        } else if (val == "Rating") {
          this.restaurantForTheCuisine.sort(function(a, b) {
            return a.AggregateRating - b.AggregateRating;
          });
        } else if (val == "Votes") {
          this.restaurantForTheCuisine.sort(function(a, b) {
            return a.Votes - b.Votes;
          });
        } else {
          this.restaurantForTheCuisine.sort(function(a, b) {
            return a.AverageCostForTwo - b.AverageCostForTwo;
          });
        }

        this.AscDsc = "";
      }
    },

    AscDsc: {
      handler(val, oldVal) {
        if (val == "") {
          this.AscDsc = oldVal;
        } else if (val == "DSC") {
          this.restaurantForTheCuisine.reverse();
        } else if (val == "ASC" && oldVal == "DSC") {
          this.restaurantForTheCuisine.reverse();
        }
      }
    }
  }
};
</script>

<style>
#restaurants {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background-color: rgba(19, 83, 179, 0.404);
}
#sc {
  height: 400px;

  overflow-y: scroll;
}
</style>