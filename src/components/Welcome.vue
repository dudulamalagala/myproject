<template>
	<div>
		<h1>WELCOME TO DASHBOARD</h1>
		<h1>{{ msg }}</h1>
		<button @click="goToHome()">Sign out</button>
	</div>
</template>

<script>
import router from '../router/index.js'
import axios from 'axios';

const url = "http://localhost:8080/getUserInfo";
var msg;

export default {
	name: 'Welcome',
	data() {
		axios.get(url)
		  .then(function (response) {
			msg = response.data
		  })
		  .catch(function (error) {
			alert(error);
		  });
		return {
			msg
		}
	},
	methods:{
	    goToHome: () => {
			router.push('/home'); 
		}
	}
}
</script>