<template>
	<div>
		<h2>Add new user</h2>
		<form action="/users" method="post" class="form-horizontal">
			
			<div class="form-group">
				<label for="name" class="control-label col-sm-2">Name : </label>
				<div class="col-sm-10">
					<input type="text" name="name" id="name" value="" class="form-control" placeholder="Enter name" v-model="name" />
					<span v-if="errors.name" class="error">{{ errors.name[0] }}</span>
				</div>
			</div>

			<div class="form-group">
				<label for="email" class="control-label col-sm-2">Email : </label>
				<div class="col-sm-10">
					<input type="email" name="email" id="email" value="" class="form-control" placeholder="Enter email" v-model="email" />
					<span v-if="errors.email" class="error">{{ errors.email[0] }}</span>
				</div>
			</div>

			<div class="form-group">
				<label for="password" class="control-label col-sm-2">Password : </label>
				<div class="col-sm-10">
					<input type="password" name="password" id="password" value="" class="form-control" placeholder="Enter password" v-model="password" />
					<span v-if="errors.password" class="error">{{ errors.password[0] }}</span>
				</div>
			</div>

			<div class="form-group">
				<div class="col-sm-offset-2 col-sm-10">
					<button type="button" class="btn btn-default" v-on:click="addNewUser()">Save</button>
				</div>
			</div>
		
		</form>
	</div>
</template>

<script>
	export default {
		data(){
			return {
				name:'',
				email:'',
				password:'',

				sendVar:{},

				errors:[],
			}
		},
		methods:{
			addNewUser(){
				this.errors = [];
				console.log(this.name)
				console.log(this.email)
				console.log(this.password)

				this.sendVar.name = this.name;
				this.sendVar.email = this.email;
				this.sendVar.password = this.password;
				axios.post('/api/users/', this.sendVar)
				.then(response=>{
					console.log(response);

					this.name = '';
					this.email = '';
					this.password = '';
				})
				.catch(error => {
					console.log(error);

					if( error.response.status == 422 ){
						this.errors = error.response.data.errors
					}
				});
			}
		}
	}
</script>

<style>
	.error{
		color:red;
	}
</style>