<template>
    <div class="vue-tempalte">
        <form name="form1" class="form-signin">
            <h3>Sign In</h3>

            <div class="form-group">
                <label>User Name</label>
                <input type="text" v-model="username" id="username" class="form-control form-control-lg" />
            </div>

            <div class="form-group">
                <label>Password</label>
                <input type="password" v-model="password" id="password" class="form-control form-control-lg" />
				{{ errorMsg }}
            </div>
            <button type="submit" v-on:click="showAlert" class="btn btn-dark btn-lg btn-block">Sign In</button>

        </form>
    </div>
</template>

<script>
	import router from '../router/index.js'
	import axios from 'axios';
	
	const url = "http://localhost:8080/authenticate";
	var errorMsg;
	
    export default {
		name: 'Login',
        data() {
            return {
				username : '',
				password : ''
			}
        },
		methods: {
			showAlert: () => {
				
				const UserDetails = {
					  username: 'admin',
					  password: 'admin',
					  firstname : '',
					  lastname : ''
					};
				
				axios.post(url, UserDetails)
				  .then(function (response) {
					if (response.data === "success") {
						router.push('/welcome');
				    } else {
						alert("Authentication failure");
						errorMsg = 'Your username and password are invalid.'
				    }
				  })
				  .catch(function (error) {
					alert(error);
				  });
			}
		}
    }
</script>