<template>
<section>
  <div class="tbl-header">
    <table cellpadding="0" cellspacing="0" border="0">
      <thead>
        <tr>
          <th>Id</th>
          <th>Nome</th>
          <th>Preço</th>
          <th>Descrição</th>
          <th>Açoes</th>
        </tr>
      </thead>
    </table>
  </div>
  <div class="tbl-content">
    <table cellpadding="0" cellspacing="0" border="0">
      <tbody>
        <tr>
          <td>{{ planta.id }}</td>
          <td>{{ planta.nome }} </td>
          <td>{{ planta.preco }},00</td>
          <td>{{ planta.descricao }}</td>
          <td> 
            <router-link :to="getPlantaUrl(planta.id)">
            <button class="btnEdit">
              <span>
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24"><path fill="none" d="M0 0h24v24H0z"></path><path fill="currentColor" d="M11 11V5h2v6h6v2h-6v6h-2v-6H5v-2z"></path></svg> 
                Edit
              </span>
            </button>
          </router-link>
            <button class="btnDelete" @click="deletePlantas">
              <span>
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24" height="24"><path fill="none" d="M0 0h24v24H0z"></path><path fill="currentColor" d="M11 11V5h2v6h6v2h-6v6h-2v-6H5v-2z"></path></svg> 
                Delete
              </span>
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</section>
</template>

<script>
  import axios from "axios"
  export default {
   props: ["planta"],
   data() {
     return {
       plantas: [],
     };
   },
   methods: {
    async getPlantas() {
        axios
         .get(`https://localhost:44372/api/Plantas`)
        .then((res) => {
           this.plantas = res.data;
         })
         .catch((error) => {
           console.log(error);
         });
   },
   async deletePlantas() {
        axios
        .delete(`https://localhost:7219/api/Plantas/${this.planta.id}/`,{
          headers: { "Content-Type": "multipart/form-data" }
		 })
         .then((res) => {
          this.plantas = res.data;
         })
         .catch((error) => {
           console.log(error);
         });
         this.getPlantas()
   },
   getPlantaUrl(id) {
      return `/edit/${id}`;
    },
  }
}

  </script>

<style>

table{
  width:100%;
  table-layout: fixed;
}
.tbl-header{
  background-color: rgba(255,255,255,0.3);
 }
.tbl-content{
  overflow-x:auto;
  margin-top: 0px;
  border: 1px solid rgba(255,255,255,0.3);
}
th{
  padding: 20px 15px;
  text-align: left;
  font-weight: 500;
  font-size: 12px;
  color: #fff;
  text-transform: uppercase;
}
td{
  padding: 15px;
  text-align: left;
  vertical-align:middle;
  font-weight: 500;
  font-size: 15px;
  color: #fff;
  border-bottom: solid 1px rgba(255,255,255,0.1);
}


/* demo styles */
section{
  margin: 50px;
}


/* follow me template */
.made-with-love {
  margin-top: 40px;
  padding: 10px;
  clear: left;
  text-align: center;
  font-size: 10px;
  font-family: arial;
  color: #fff;
}
.made-with-love i {
  font-style: normal;
  color: #F50057;
  font-size: 14px;
  position: relative;
  top: 2px;
}
.made-with-love a {
  color: #fff;
  text-decoration: none;
}
.made-with-love a:hover {
  text-decoration: underline;
}


/* for custom scrollbar for webkit browser*/

::-webkit-scrollbar {
    width: 6px;
} 
::-webkit-scrollbar-track {
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
} 
::-webkit-scrollbar-thumb {
    -webkit-box-shadow: inset 0 0 6px rgba(0,0,0,0.3); 
}
.btnEdit {
 border: 1px solid #24b4fb;
 background-color: #24b4fb;
 border-radius: 0.3em;
 padding: 0.3em 0.8em 0.3em 0.6em;
 transition: all ease-in-out 0.2s;
 font-size: 16px;
 cursor: pointer;
 margin-left: 10px;
}

.btnEdit span {
 display: flex;
 justify-content: center;
 align-items: center;
 color: #fff;
 font-weight: 600;
}

.btnEdit:hover {
 background-color: #0071e2;
}
.btnDelete {
 border: 1px solid #ff4242af;
 background-color: #ff4242af;
 border-radius: 0.3em;
 padding: 0.3em 0.8em 0.3em 0.6em;
 transition: all ease-in-out 0.2s;
 font-size: 16px;
 cursor: pointer;
 margin-left: 10px;
}

.btnDelete span {
 display: flex;
 justify-content: center;
 align-items: center;
 color: #fff;
 font-weight: 600;
}
.btnDelete:hover {
  border: none;
 background-color: #ff0000af;
}


</style>