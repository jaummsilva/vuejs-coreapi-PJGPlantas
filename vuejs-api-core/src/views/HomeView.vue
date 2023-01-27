<template>
  <div>
    <h1>Plantas</h1>
    <Plantas 
    v-for="planta in plantas" :key="planta.id" :planta="planta" />
  </div>
</template>

<script>
import axios from "axios";
import Plantas from "../components/Plantas.vue";
export default {
  name: 'App',
  components: {Plantas},
  data() {
    return {
      planta: {},
      plantas: [],
    };  
  },
  async created() {
    await this.getPlantas();
  },
  methods: {
    async getPlantas() {
        axios
         .get(`https://localhost:44332/api/Plantas/`)
         .then((res) => {
           this.plantas = res.data;
         })
         .catch((error) => {
           console.log(error);
         });
   },
  }
}
</script>

<style>
.planta {
  height: 1000px;
}
h1{
  font-size: 30px;
  color: #fff;
  text-transform: uppercase;
  font-weight: 300;
  text-align: center;
  margin-bottom: 15px;
}

body{
  background: -webkit-linear-gradient(left, #25c481, #25b7c4);
  background: linear-gradient(to right, #25c481, #25b7c4);
  font-family: 'Roboto', sans-serif;
}
</style>
