<template>
	<main class="slideshow">

		<div class="slideshow__images">
			<figure class="slideshow__images">
			<img class="slideshow__image" :src="startImage.file" :alt="startImage.caption" >
			<figcaption class="slideshow__images-caption">{{ startImage.caption }}</figcaption>
			</figure>
		</div>
		<div class="slideshow__buttons">
			<button class="slideshow__buttons-previous"  @click="previous" > Previous</button>
			<button class="slideshow__buttons-next" @click="next" > Next</button>
		</div>
		<!-- v-if="currentIndex > 0" -->
		<!-- v-if="currentIndex < 7" -->
	</main>

</template>

<script>
	export default {
		data() {
			return {
			currentIndex: 0,
			image: [
				{caption: 'Emil Adolf von Behring', file: '/images/EmilB.jpg'},
				{caption: 'Hermann Emil Fischer', file: '/images/EmilF.jpg'},
				{caption: 'Jean Henry Dunant', file: '/images/Henri.jpg'},
				{caption: 'Sully Prudhomme', file: '/images/Sully.jpg'},
				{caption: 'Christian Matthias Theodor Mommsen', file: '/images/Theodor.jpg'},
				{caption: 'Wilhelm Conrad Röntgen', file: '/images/Wilhelm.jpg'},
				{caption: 'Élie Ducommun', file: '/images/Eli.jpg'},
				{caption: 'Jacobus Henricus vant Hoff', file: '/images/jacobush.jpg'},
			],
			
			};
	   },
		computed: {
			startImage() {
				return this.image[this.currentIndex];
		},

		methods: { 
			next() {
				this.currentIndex = this.currentIndex === this.image.length - 1 ? 0 : this.currentIndex + 1;
		},
			previous() {
				this.currentIndex = this.currentIndex === 0 ? this.image.length - 1 : this.currentIndex - 1;
			},
	 	}
 	 }
	}
</script>

<style scoped>


	.slideshow__images-caption {
		text-align: center;
		background-color: #f4f2f0;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		padding: 10px;
		width: 250px;
		margin-top: 10px;
		margin-left: 550px;
		color: #bb8a35;
		font-weight: bold;

	}

	.slideshow__buttons {
		display: flex;
		justify-content: space-between;
		position: relative;
	}


	.slideshow__buttons-next {
		text-align: center;
		background-color: #f4f2f0;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		padding: 8px;
		width: 100px;
		margin-right: 35px;
		color: #bb8a35;
		font-weight: bold;
	}

	.slideshow__buttons-previous {
		text-align: center;
		background-color: #f4f2f0;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		padding: 8px;
		width: 100px;
		margin-left: 35px;
		color: #bb8a35;
		font-weight: bold;
		
	}

	.slideshow__image {
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		width: 70vw;
		height: 70vh;
		margin-left: 160px;
	
	}
</style>