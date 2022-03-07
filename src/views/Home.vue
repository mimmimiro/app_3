<template>
<main >
	<Header />
	<Slideshow />
	<!-- <div class="search"> 
        <input 
          type="text" 
          class="search__input" 
          placeholder="Search..."
          v-model="search">
			 <span>{{ yearValue }}</span>
			 <span>{{ winnerName }}</span>
			 <button @click="searchWinner" class="search__button">winner year</button>
	 </div> -->
			<div v-if="error">{{ error }}</div>
	<section class="container">
		<ul class="container__list" v-for="winner in winners" :key="winner.id"> 
				<li class="container__list-award">{{ year }} {{winner.awardYear}}</li>
				<li class="container__list-prize">{{ prize }}{{ winner.prizeAmount }}</li>
				<li class="container__list-category">{{ category }} {{ winner.categoryFullName.en }} </li>
				<li  class="container__list-laureate" v-for="laureate in winner.laureates" :key="laureate.id">
				{{laureate.fullName.en}}: <br> {{ laureate.motivation.en}}</li>
		</ul>
	</section>
	
		</main>
</template>

<script>
	import Slideshow from '../components/Slideshow.vue'
	import Header from '../components/Header.vue'
	export default {
			components:{
				Header,
				Slideshow
			},
		data() {
				return {
					error:'',
					year: 'Award year:',
					prize: 'Prize amount: $',
					category: 'Category:',
					fullName: '',
				//  search: '',
				//  yearValue: '',
					winners: [],
				//   winnerName: '',
					motivation:'',
					laureates: []
				}
			},
		created() {
				this.fetchWinner();
			},
		methods: {
				async fetchWinner() {
				const url = 'https://masterdataapi.nobelprize.org/2.1/nobelPrizes?offset=0&limit=8';
				try {
					await this.handleResponse(url);
				} catch (error) {
					console.log(error)
					this.error = error;
				}
		
				},
		async handleResponse(url) {
				const response = await fetch(url); 
				console.log(response)
				if(response && response.status >= 200 && response.status < 300) {
					const { nobelPrizes  }  = await response.json();
					this.winners = nobelPrizes;
					this.laureates = this.winners[0].laureates;
					return true;
				} else {
					throw new Error('Error galt')
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
		margin: 25px;
		background-color: #f4f2f0;
		line-height: 1.8rem;
		font-family: sans-serif;
		
	}

	.container__list {
		margin: 25px;
	}

	li {
	list-style: none;
	}

	.container__list-award {
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		background-color: #bb8a35;
		padding: 10px;
		font-weight: 500;
	}

	.container__list-category,
	.container__list-prize,
	.container__list-laureate {
		padding: 5px;
	}
</style>

