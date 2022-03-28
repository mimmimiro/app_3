<template>
	<main >
		<Header />
		<Slideshow />

	      <!-- The error message only appears when error is detected -->
			<div v-if="error">{{ error }}</div>
      	<!-- the buttons switches the list between hiding and showing -->
			<button @click="showWinners" v-if="!winnersAreVisible">Show Winners</button>
			<button @click="hideWinners" v-else>Hide Winners</button>

			<section class="container" v-if="winnersAreVisible === true">
					<ul class="container__list" v-for="winner in winners" :key="winner.id"> 
					<li class="container__list-award">{{ year }} {{winner.awardYear}}</li>
					<li class="container__list-prize">{{ prize }}{{ winner.prizeAmount }}</li>
					<li class="container__list-category">{{ category }} {{ winner.categoryFullName.en }} </li>
					<li  class="container__list-laureate" v-for="laureate in winner.laureates" :key="laureate.id">
					{{laureate.fullName.en}}: <br> {{ laureate.motivation.en}}</li>
				</ul>
			</section>
		<Footer />
		</main>
</template>

<script>
	import Slideshow from '../components/Slideshow.vue'
	import Header from '../components/Header.vue'
	import Footer from '../components/Footer.vue'
	export default {
			components:{
				Header,
				Slideshow,
				Footer
			},
		data() {
				return {
					error:'',
					year: 'Award year:',
					prize: 'Prize amount: $',
					category: 'Category:',
					fullName: '',
					winners: [],
					motivation:'',
					laureates: [],
					winnersAreVisible: false,
				}
			},
		created() {
				this.fetchWinner();
			},
		methods: {
			showWinners() {
				this.winnersAreVisible = true;
			},
			hideWinners() {
				this.winnersAreVisible = false;
			},
			  //  an asynchronous HTTP request in JavaScript/vue with the deconstructed fetch method
			  // it offers an eloquent way to establish agile communication between client and server.
			 // fetch returns a promise, wich allows us to handle the asynchronous request in a smarter way
				async fetchWinner() {
				const url = 'https://masterdataapi.nobelprize.org/2.1/nobelPrizes?offset=0&limit=8';
				try {
					await this.handleResponse(url);
				} catch (error) {
					console.log(error)
					this.error = error;
				}
		
				},
			// The catch() function is only used if fetch() could not send a request. This typically means that there was an error
			async handleResponse(url) {
				const response = await fetch(url); 
				if(response && response.status >= 200 && response.status < 300) {
					const { nobelPrizes  }  = await response.json();
					this.winners = nobelPrizes;
					this.laureates = this.winners[0].laureates;
					return true;
				} else {
					if(response.status === 404) {
					throw new Error('Url is not right');
				}
					if(response.status === 500) {
					throw new Error('server not working!');
				}
					throw new Error('Fatal Error')
				}
		}	
	}
}

</script>

<style scoped>
 
	.container {
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		display: flex;
		flex-direction: column;
		margin: 20px 75px;
		background-color: #f4f2f0;
		line-height: 1.6rem;
	}

	.container__list {
		margin: 15px;
	}

	li {
		list-style: none;
	}

	.container__list-award {
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		background-color: #bb8a35;
		padding: 10px;
		border-radius: 5px;
		font-weight: 600;
		color: rgb(44, 44, 44);
		letter-spacing: 0.1em;
	}

	.container__list-category,
	.container__list-prize,
	.container__list-laureate {
		padding: 5px;
	}

	button {
		text-align: center;
		background-color: #bb8a35;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		padding: 10px;
		border-radius: 5px;
		width: 200px;
		margin-left: 600px;
		color: #f4f2f0;
		font-weight: bold;
		cursor: pointer;
		letter-spacing: 0.15em;
	}
   /* small and medium devices */
	@media screen and (max-width: 1024px) {
		.container__list,
		.container__list-category,
		.container__list-prize,
		.container__list-laureate {
			padding: 5px;
			line-height: 3.5rem;
		}
		.container__list-laureate {
			background-color:  #d4c3a5;
		}
		button {
			margin-left: 450px;
		}
	}
</style>

