<template>
	<section class="container">
		<header class="container__footer">
			<span class="container__footer-title">{{ title }}</span>
		</header>	
	</section>

</template>


<script>
	export default {
		data() {
			return {
			title: '@CartaDesign'
			}
		},
	}
</script>

<style scoped>
	.container {
		display: grid;
		grid-template-columns: var(--grid-column-12);
		gap: 1rem;
		
	}

	.container__footer {
		box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
		background-color: #f4f2f0;
		grid-column: 1/ span 12;
		display: grid;
		height: 150px;
	}

	.container__footer-title {
		grid-column: 1/ span 2;
		font-size: 1.4rem;
		color: #bb8a35;
		padding-top: 30px;
		line-height: 1.4rem;
		margin: 25px 5px;
	}
</style>