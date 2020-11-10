<template>
	<div>
		<div class="text-center" id="jumbotron">
			<div class="card-jumbo">
				<h1 class="display-4">Motorcycle rental made easy</h1>
				<p class="lead">Malaysia's first motorbike sharing. Insurance available for all!</p>

				<div class="row row-cols-lg-auto g-3 align-items-center justify-content-center">
					<div class="col-12">
						<label for="inlineFormInputGroupUsername">Where
						</label>
						<select class="form-select" id="inlineFormSelectPref" :v-model="citySelected">
							<option v-for="city in cities" :key="city.id">{{city.name}}</option>
						</select>
					</div>

					<div class="col-12">
						<label for="inlineFormInputGroupUsername">Pick up date
						</label>
						<div class="input-group">
							<input type="date" class="form-control" id="inlineFormInputGroupUsername" placeholder="Pickup date" v-model="pickupdate">
						</div>
					</div>

					<div class="col-12">
						<label for="inlineFormInputGroupUsername">Return date
						</label>
						<div class="input-group">
							<input type="date" class="form-control" id="inlineFormInputGroupUsername" placeholder="Return date" v-model="returndate">
						</div>
					</div>

					<div class="col-12">
						<button type="submit" class="btn btn-primary" v-on:click="searchClick">Search</button>
					</div>
				</div>
			</div>
		</div>

		<section id="featured-bikes" class="py-5">
			<div class="container">
				<h3>Featured Bikes</h3>
				<div class="row">
					<div class="col-4" v-for="motor in motorbikes" :key="motor.name" v-on:click="detailClick(motor.id)">
						<div class="card">
							<img v-bind:src="motor.img" class="card-img-top" alt="..." width="460" height="280">
							<div class="card-body">
								<h5 class="card-title">{{motor.name}}</h5>
								<p class="card-text"><i class="fas fa-map-marker-alt"></i>{{motor.location}}</p>
							</div>
						</div>
					</div>

				</div>
			</div>
		</section>

		<section id="easy-rental" class="bg-warning py-5 text-center">
			<h3>Easy Motorcycle Rental</h3>
			<hr style="width:500px; margin:0 auto" class="my-3">
			<div class="row">
				<div class="col-4">
					<h2 class="rental-icon"><i class="fas fa-serach"></i></h2>
					<h5>Choose a bike</h5><p>Over 100+ motorcycles listed! Rent the one that suits you.</p>
				</div>

				<div class="col-4">
					<h2 class="rental-icon"><i class="fas fa-calender-alt"></i></h2>
					<h5>Book your trip</h5><p>Register your account, select bike and pay.</p>
				</div>

				<div class="col-4">
					<h2 class="rental-icon"><i class="fas fa-motorcycle"></i></h2>
					<h5>Go for a ride</h5><p>Protection options, insurance & unlimited kilometers</p>
				</div>
			</div>
		</section>

		<section id="video" class="bg-light py-5 text-center">
			<h3>Learn about us</h3>
			<hr style="width: 500px; margin:0 auto" class="my-3">
			<iframe width="560" height="315" src="https://www.youtube.com/embed/UY0QY__2ESQ" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
		</section>
	</div>
</template>

<script>
export default {
	name: 'Main',
	mounted(){
		alert('Page Loading!')
		let url = 'https://api.sheety.co/6a294e74779b4334bc93620758fe8c26/motors/sheet1';
		fetch(url)
		.then((response) => response.json())
		.then(json => {
  // Do something with the data
  // // this.motorbikes = json.sheet1 <- If this code applied that meant will get all data and image from the googlesheet
  this.motorbikes = json.sheet1
  // console.log(json.sheet1);
});
  
},

data(){
	return{
		//This is local info. Maybe need change to get from googlesheet
		motorbikes:[
		//If want use local image can use to define name, location and image as below
		// {
		// 	name:"Harley Davidson Fatboy",
		// 	location:"Seremban Bandar Sri Sendayan, Negeri Sembilan",
		// 	img:"../images/HarleyDavidsonFatboy.jpg"
		// },
		// {
		// 	name:"Yamaha 135C",
		// 	location:"Putrajaya Central, Selangor",
		// 	img:"../images/yamaha.jpg"
		// },
		// {
		// 	name:"KTM 250 TPI",
		// 	location:"Damansara Perdana Selangor",
		// 	img:"../images/KTM250TPI.jpg"
		// }
		],

		cities:[
		{
			id:'1',
			name:"Seremban"
		},
		{
			id:'2',
			name:"Kuala Lumpur"
		},
		{
			id:'3',
			name:"Melaka"
		},
		{
			id:'4',
			name:"Perak"
		}
		],

		pickupdate:'',
		returndate:'',
		citySelected:'Seremban'
	}
},

methods:{
	detailClick: function(id){
		console.log(id)
		this.$router.push({name:'Car',params:{id:id}})
	},

	searchClick: function(){

			//To do this also need update in index.js
			this.$router.push({name:'Detail',params:{sendDate:this.pickupdate,returnDate:this.returndate,city:this.citySelected}})

			// console.log('user select '+this.pickupdate+ ' ' + this.returndate+ ' ' + this.citySelected)

			// window.location.href = "/detail"+this.pickupdate+"/"+this.returndate+"/"+this.citySelected
		}
	}
	// 	getImgUrl: function(url){
	// 		var images = require.contennt('../asset/', false, /\.jpg$/)
	// 		return images('./' + pet + ".jpg")
	// 	}
	// }
}


</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#jumbotron {
	background-image: url('../../public/images/jumbos.jpg');
	background-size: cover;
	height: 80%;
	padding-top: 150px 0px;
	color: white;
}

.card-jumbo {
	border-radius: 15px;
	background-color: rgba(0,0,0,0.5);
	width: 60%;
	margin: 0px auto;
	padding: 30px;
}

h3{
	margin: 40px 0 0;
}


.rental-icon{
	font-size: 72px;
}
</style>