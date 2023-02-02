<template id="registerTemplate">
	<div class="content">
	  <form @submit.prevent='onSubmit' ref='form' action="" class='register-form'>
			<h2>Register</h2>
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
			<br>
			<hr>
			<br>
			<div class="form-group"> 
				<input type="submit" value='Register' @click="postPlantas">
			</div>
	  </form>
	</div>
 </template>

<script>
import axios from "axios";
export default {
  name: 'App',
  data() {
    return {
      planta: {
		nome : "",
		preco : "",
		descricao: "",
	  },
      plantas: [],
    };  
  },
  methods: {
    async postPlantas() {
        axios
         .post(`https://localhost:7219/api/Plantas`, this.planta, {
			headers: {'Content-Type': 'application/json'}
		 })
         .then((res) => {
           this.planta = res.data;
		   alert("Planta criada com sucesso");
		   this.$router.push('/');
         })
         .catch((error) => {
           console.log(error);
         });
   },
  }
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css?family=PT+Sans');

*, *::before, *::after {
	box-sizing: border-box;
}

.content {
	padding: 0;
	font-family: 'PT Sans', sans-serif;
	background: linear-gradient(90deg, #3F2B96 0%, #61729b 100%);
	display: flex;
	flex-direction: column;
	justify-content: center;
	margin-top:2%;
}
hr {
	width: 250px;
	display: flex;
	flex-direction: row;
	justify-content: center;
	border: 1px solid rgb(255, 255, 255);
}

.register-form h2 {
	font-size: 25pt;
	color: #ffffff;
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
		opacity: .4;
}


form h2, header h2 {
	text-align: center;
	color:var(--brandColor);
}

.register-form {
	padding:1em;
}

.form-group {
	display: flex;
	flex-direction: row;
	flex-wrap: wrap;
	justify-content:center;
	padding:8px;
}
.form-group	label {
		text-align: right;
		margin-right: 2em;
		color: #ffffff;
	}
	
	input {
		font-size: inherit;
		border-style: none none solid none;
		background:whitesmoke;
		font-family:inherit;
		padding:.4em;
		width: 400px;
	}
	

.feedback {
	padding: 1em;
}
	

form 
	
	input[type=submit] {
		display: block;
		font-size: inherit;
		cursor: pointer;
		background-color: #ffffff;
		color:rgb(0, 0, 0);
		border:none;
		height: 50px;
		width: 100px;
	}
	
	input[type=submit]:disabled {
		opacity: .4;
		cursor: not-allowed;
	}
	
	input[type=submit]:hover {
		background-color: #9b9b9b;
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
