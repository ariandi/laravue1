<template>
	<div>
		<h2>Edit user</h2>
		<form action="/users" method="post" class="form-horizontal">
			
			<div class="form-group">
				<label for="name" class="control-label col-sm-2">Name : </label>
				<div class="col-sm-10">
					<input type="text" name="name" id="name" value="" class="form-control" placeholder="Enter name" v-model="name" />
				</div>
			</div>

			<div class="form-group">
				<label for="email" class="control-label col-sm-2">Email : </label>
				<div class="col-sm-10">
					<input type="email" name="email" id="email" value="" class="form-control" placeholder="Enter email" v-model="email" />
				</div>
			</div>

			<div class="form-group">
				<div class="col-sm-offset-2 col-sm-10">
					<button type="button" class="btn btn-default" v-on:click="updateUser()">Update</button>
				</div>
			</div>
		
		</form>
	</div>
</template>

<script>
	export default {
		props: ['id'],
		data(){
			return {
				name:'',
				email:'',

				sendVar:{},
			}
		},
		mounted() {
        console.log('Component mounted.');
        this.editUser();
    },
		methods:{
			editUser(){
				axios.get('/api/users/'+this.id)
				.then(resp=>{
					console.log(resp);
					var user = resp.data;
					this.name = user.name;
					this.email = user.email;
				})
			},

			updateUser(){
				console.log(this.name)
				console.log(this.email)

				this.sendVar.name = this.name;
				this.sendVar.email = this.email;
				axios.put('/api/users/'+this.id, this.sendVar)
				.then(response=>{
					console.log(response);
				})
				.catch(error => {
					console.log(error);
				});
			}
		}
	}
</script>

