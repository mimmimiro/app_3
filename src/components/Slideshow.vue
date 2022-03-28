<template>
	<main class="slideshow">
			<figure class="slideshow__images">
				 <!-- transtion-group component in Vue.js,  images will iterate.-->
				<transition-group name="slide" tag="ul">
					<section class="slideshow__timer" v-for="image in [currentIndex]" :key="image">
			<img class="slideshow__image" :src="startImage.file" :alt="startImage.caption" >
			<figcaption class="slideshow__images-caption">{{ startImage.caption }}</figcaption>
					</section>
					</transition-group>
			</figure>
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
			image: [
				{caption: 'Emil Adolf von Behring', file: '/images/EmilB.jpg'},
				{caption: 'Hermann Emil Fischer', file: '/images/EmilF.jpg'},
				{caption: 'Jean Henry Dunant & Frédéric Passy', file: '/images/Henri.jpg'},
				{caption: 'Sully Prudhomme', file: '/images/Sully.jpg'},
				{caption: 'Christian Matthias Theodor Mommsen', file: '/images/Theodor.jpg'},
				{caption: 'Wilhelm Conrad Röntgen', file: '/images/Wilhelm.jpg'},
				{caption: 'Élie Ducommun & Charles Albert Gobat', file: '/images/ElieD.jpg'},
				{caption: 'Jacobus Henricus vant Hoff', file: '/images/jacobush.jpg'},
			],
			timer: null,
			currentIndex: 0
			
			};
	   },
		mounted() {
    			this.startSlideshow();
  		},
		//   the slides glide every 6 seconds with this method
		methods: { 
			startSlideshow() {
      		this.timer = setInterval(this.next, 6000);
    		},
			next() {
				console.log('next')
			   this.currentIndex = this.currentIndex === this.image.length - 1 ? 0 : this.currentIndex + 1;
				
			},
			previous() {
				this.currentIndex = this.currentIndex === 0 ? this.image.length - 1 : this.currentIndex - 1;
				
			},
	 	},
		computed: {
			startImage() {
				return this.image[this.currentIndex];
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
		border-radius: 5px;
		width: 470px;
		margin: 15px 0px 20px 550px;
		color: #bb8a35;
		font-weight: bold;
		letter-spacing: 0.15em;
	}
	.slideshow__buttons {
		display: flex;
		justify-content: space-between;
		
	}
	.slideshow__buttons-next {
		text-align: center;
		background-color: #f4f2f0;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		padding: 10px;
		width: 120px;
		margin-right: 45px; 
		color: #bb8a35;
		font-weight: bold;
		cursor: pointer;
		letter-spacing: 0.15em;
		border-radius: 5px; 
		right: 0;
	}
	.slideshow__buttons-previous {
		text-align: center;
		background-color: #f4f2f0;
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		padding: 10px;
		border-radius: 5px;
		width: 120px;
		margin-left: 45px;
		color: #bb8a35;
		font-weight: bold;
		cursor: pointer;
		letter-spacing: 0.15em;
		left: 0;
	}
	.slideshow__image {
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		width: 70vw;
		height: 70vh;
		margin-left: 210px;
	
	}
	/* apply transition to moving elements */

	.slide-enter-active,
	.slide-leave-active {
		transition: all 0.5s ease;
	}

	.slide-enter-from,
	.slide-leave-to {
		opacity: 0;
		transform: translateX(30px);
	}

	.slide-leave-active {
		position: absolute;
	}
	.slide-move {
		transition: transform 0.8 ease;
	}
	/* small and medium devices */
	@media screen and (max-width: 1024px) {
		.slideshow__image {
			width: 80vw;
			height: 60vh;
			margin: 10px 10px 10px 90px;
		}
		.slideshow__images-caption {
			margin: 10px 200px 10px 300px;
		}
		.slideshow__buttons-previous,
		.slideshow__buttons-next {
			top: 77%;
		}
	
	}
</style>