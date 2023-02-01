<template id="registerTemplate">
  <body>
	  <form @submit.prevent='onSubmit' ref='form' action="" class='register-form'>
			<h2>Edit</h2>
			<div class="form-group" >
				 <label>Name</label>
				 <input placeholder="Name" v-model="planta.nome">
			</div>
			<div class="form-group">
				 <label>Price</label>
				 <input placeholder="Price" v-model="planta.preco">
			</div>
			<div class="form-group">
				 <label>Description</label>
				 <input placeholder="Description" v-model="planta.descricao">
			</div>
			<input type="submit" value='Register' @click="patchPlantas">
	  </form>
    </body>
 </template>

<script>
import axios from "axios";
export default {
  name: 'App',
  data() {
    return {
	  planta: {},
	  plantas:[]
    };  
  },
  methods: {
    async patchPlantas() {
        axios
        .put(
          `https://localhost:7219/api/Plantas/${this.planta.id}/`,
          this.plantas,
		 {headers: {'Content-Type': 'application/json'}})
         .then((res) => {
           this.plantas = res.data;
         })
         .catch((error) => {
           console.log(error);
         });
   },
	async getPlanta(id) {
      const res = await axios.get(`https://localhost:7219/api/Plantas/${id}/`);
      this.planta = res;
    },
    async created() {
    	await this.getPlanta(this.$route.params.id);
  	},
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=PT+Sans');

*, *::before, *::after {
	box-sizing: border-box;
}

:root {
	--brandColor:#008b8b;
	--brandColorDark:#057272;
}

[v-cloak] {
	opacity: 0;
}

body {
	padding: 0;
	margin: 100px;
	font-family: 'PT Sans', sans-serif;
	background:#e0e0e0;
}

#app {
	border-top:.5em solid var(--brandColor);
	max-width:800px;
	margin: 0 auto;
	position:absolute;
	top:50%;
	left:50%;
	width:96%;
	transform:translate(-50%, -50%);
	padding: 2em 3em 1em;
	background:white;
	overflow: hidden;
	box-shadow: 0 10px 6px -6px rgba(0,0,0,.2);
	animation: enterFromBottom .7s .3s ease-out both;
	
	@media screen and (max-width:500px){
		padding: 2em 1em 1em;
	}
}

.actions button {
		all:unset;
		display: inline-block;
		padding:1em;
		letter-spacing: .05em;
		font-size: 14px;
		cursor: pointer;
		border:1px solid;
		color:white;
		border:none;
		background:var(--brandColor);
		transition:250ms; 
		margin: 0 .2em 0 0;
		opacity: .4;
}


form h2, header h2 {
	text-align: center;
	color:var(--brandColor);
}

.register-form {
	margin: 2em 0;
	padding:1em;
}

.form-group {
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	justify-content:left;
	padding:8px;
}
.form-group	label {
		flex:1;
		text-align: right;
		margin-right: 2em;
	}
	
	input {
		font-size: inherit;
		border:none;
		background:whitesmoke;
		font-family:inherit;
		padding:.4em;
		flex:1.5;
	}
	
	input.invalid {
		border:1px solid tomato;
	}

.feedback {
	padding: 1em;
}
	
.feedback	p {
		line-height: 1.4;
		max-width:50ch;
		margin: 10px auto;
		text-align:center;
}

form 
	
	input[type=submit] {
		display: block;
		margin: 2em 0 2em 25em;
		padding: .6em 1em;
		font-size: inherit;
		cursor: pointer;
		background-color: #057272;
		color:rgb(255, 255, 255);
		border:none;
	}
	
	input[type=submit]:disabled {
		opacity: .4;
		cursor: not-allowed;
	}
	
	input[type=submit]:hover {
		background: var(--brandColorDark);
	}
	

@keyframes enterFromBottom {
	0%  {
		opacity:0;
		transform:translate(-50%, -45%);
	}
	100% {
		opacity:1;
		transform:translate(-50%, -50%);
	}
}


</style>
