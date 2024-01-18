<template>


<!-- Task 1 -->
    <div class="container">
      <rout-component v-for="rout in this.routes" :id="rout.id" :from="rout.fromcity" :to="rout.tocity" :cost="rout.cost" :time="rout.departuretime" :date="rout.departuredate"></rout-component>
  </div>
</template>


<script>
import Rout from './Rout.vue';

export default {
  name: "AllRoutes",
  data() {
    return {
      toTallinn: 0,
      routes: [],

    };
  },
  methods: {
    fetchRouts() {
      fetch(`http://localhost:3000/api/routes/`)
        .then((response) => response.json())
        .then((data) => (this.routes = data))
        .catch((err) => console.log(err.message));
   },
  },
  mounted() {
    this.fetchRouts();
    console.log("mounted");
  },
  components:{
    "rout-component":Rout
  } 
};
</script>

<style scoped>
.container{
  display: flex;
  flex-direction: column;
  padding-left: 20%;
  padding-right: 20%;
  
}
h1 {
  font-size: 20px;
}

</style>