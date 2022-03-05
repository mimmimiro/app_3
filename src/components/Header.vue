<template>
<section class="container">
 <header class="container__header">
 <span class="container__header-title">{{ title }}</span>
  
	</header>	
</section>

</template>


<script>
export default {
	data() {
		return {
       title: 'THE NOBEL PRIZE'
		  
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

.container__header {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  background-color: #f4f2f0;
  grid-column: 1/ span 12;
  display: grid;
  height: 210px;
  /* padding-top: 10px; */
  /* margin-bottom: 5px; */
}

.container__header-title {
	grid-column: 3/ span 2;
	font-size: 3rem;
	color: #bb8a35;
	padding-top: 40px;
	font-family:sans-serif;
	line-height: 1.6rem;
	margin: 45px 5px;
	
	
}





</style>