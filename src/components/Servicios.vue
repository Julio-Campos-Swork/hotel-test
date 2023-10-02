<template>
	<hr class="border-white opacity-70" />
	<!-- <section id="servicios" class="secondBGColor"> -->
	<h1
		class="text-center text-white text-xl lg:text-4xl pt-10 uppercase px-2 subTitleFont"
	>
		Conoce Nuestros Servicios
	</h1>
	<Carrousel :timeMS="5000" :data="serviciosData.servicio" :hasManyPhotos="true" />
	<!-- </section> -->
</template>

<script setup>
	import serviciosData from '../data/serviciosData.json'
	import Carrousel from './Carrousel/Carrousel.vue'
</script>

<style scoped></style>
