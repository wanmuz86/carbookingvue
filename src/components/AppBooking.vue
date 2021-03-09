<template>
	<div class="home">
		<app-toolbar></app-toolbar>
		<v-container>
			<h1>Booking information</h1>
			<v-alert
			type="success" v-if="message !=''">{{message}}</v-alert>
			<v-alert
			type="error"
			v-if="error !=''"
			>{{error}}</v-alert>
			<v-card class="pa-5">
				<v-text-field
				label="Name"
				v-model="name"
				></v-text-field>
				<v-row>
					<v-col cols="6">
						<v-text-field
						type="email"
						label="Email"
						v-model="email"
						></v-text-field>
					</v-col>
					<v-col cols="6">
						<v-text-field
						type="phone"
						label="Phone Number"
						v-model="phone"
						></v-text-field>
					</v-col>
				</v-row>
				<v-row>
					<v-col cols="6">
						<v-text-field
						type="date"
						label="Waktu Ambil"
						v-model="senddate"
						></v-text-field>
					</v-col>
					<v-col cols="6">
						<v-text-field
						type="date"
						label="Waktu Hantar"
						v-model="returndate"
						></v-text-field>
					</v-col>
				</v-row>
				<v-select
				:items="items"
				label="Lokasi ambil"
				v-model="sendplace"
				></v-select>
				<v-select
				:items="items"
				label="hantar"
				v-model="returnplace"
				></v-select>
				<v-btn block color="primary" 
				v-on:click="buttonPress"
				:loading="loading"
				>Book my car</v-btn>
			</v-card>
			
		</v-container>
		<app-footer></app-footer>
	</div>
</template>

<script>
// Step 1 : Import AppFooter and AppToolbar
import AppFooter from './AppFooter.vue';
import AppToolbar from './AppToolbar.vue';
export default {
	name: 'AppBooking',
	components: {AppFooter, AppToolbar},
	data(){
		return {
			items:["Putrajaya","Cyberjaya","Bangi","Kajang","Puchong"],
			name:'',
			email:'',
			phone:'',
			senddate:'',
			returndate:'',
			sendplace:'',
			returnplace:'',
			message:'',
			error:'',
			loading:false,
			jeniskereta:this.$route.params.carname
		}
	},
	methods: {
		buttonPress:function(){
			
			let url = 'https://api.sheety.co/4db58997dd33ab7eaa3d621c48bdea06/bookingSheets/sheet1';
			let body = {
				"sheet1": {
					"name":this.name,
					"email":this.email,
					"phone":this.phone,
					"senddate":this.senddate,
					"returndate":this.returndate,
					"sendplace":this.sendplace,
					"returnplace":this.returnplace,
					"jeniskereta":this.jeniskereta
				}
			}
			this.loading = true;
			fetch(url, {
				headers:{'Content-Type': 'application/json'},
				method: 'POST',
				body: JSON.stringify(body)
			})
			.then((response) => response.json())
			.then(json => {
				this.loading = false;
				if (json.sheet1){
					this.message = "Succesfully booked. We will contact you soon"
				}
				else {
					this.error = "Something is wrong, please try again"
				}
			});
		}
	}
  // 2) declare appfooger and apptoolbar in components
}
</script>
