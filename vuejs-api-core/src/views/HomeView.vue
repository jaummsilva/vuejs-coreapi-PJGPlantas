<template>
  <body class="bodyHome">
  <div class="contentTable">
    <h1>Plantas</h1>
    <router-link to="/create">
      <button class="btnCreate">
        <span>
              <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24"><path fill="none" d="M0 0h24v24H0z"></path><path fill="currentColor" d="M11 11V5h2v6h6v2h-6v6h-2v-6H5v-2z"></path></svg> 
                Create
          </span>
    </button>
    </router-link>
  </div>
  <div>
    <Plantas 
    v-for="planta in plantas" :key="planta.id" :planta="planta" />
  </div>
</body>
</template>

<script>
import axios from "axios";
import Plantas from "../components/Plantas.vue";
export default {
  name: 'App',
  components: {Plantas},
  data() {
    return {
      plantas: [],
    };  
  },
  async created() {
    await this.getPlantas();
  },
  methods: {
    async getPlantas() {
        axios
         .get(`https://localhost:7219/api/Plantas`)
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

<style >

.contentTable {
  display: flex;
  flex-direction: row;
  justify-content: center;
}

.btnCreate {
 border: none;
 background-color: #ffffff;
 border-radius: 0.3em;
 padding: 0.3em 0.8em 0.3em 0.6em;
 transition: all ease-in-out 0.2s;
 font-size: 16px;
 cursor: pointer;
 height: 40px;
 width: 120px;
 margin-left: 20px;
 margin-top: 15px;
}

.btnCreate span {
 display: flex;
 justify-content: center;
 align-items: center;
 color: rgb(0, 0, 0);
 font-weight: 600;
}

.btnCreate:hover {
 background-color: #a8a8a8;
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
  background: linear-gradient(to right, #69706d, #656f70);
  font-family: 'Roboto', sans-serif;
  
}
</style>
