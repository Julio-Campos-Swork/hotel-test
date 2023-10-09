<template>
	<hr class="border-white opacity-70" />
	<!-- <section id="servicios" class="secondBGColor"> -->
	<h3
		class="text-center text-white text-xl lg:text-4xl pt-10 uppercase px-2 subTitleFont"
	>
		Conoce Nuestros Servicios
	</h3>
	<Carrousel :timeMS="5000" :data="newdata" />
	<!-- </section> -->
</template>

<script setup>
	import serviciosData from '@data/serviciosData.json'
	import Carrousel from '@components/Carrousel/Carrousel.vue'
	import imagenAlberca from '@assets/Alberca.jpg'
	import imagenGimnasio from '@assets/Gimnasio.jpg'
	import imagenHabitacion from '@assets/Habitacion.jpg'
	import imagenJardin from '@assets/Jardin.jpg'
	import imagenRestaurante from '@assets/Restaurante.jpg'
	import imagenSalon from '@assets/Salon.jpg'
	import imagenSauna from '@assets/Sauna.jpg'
	import imagenTemazcal from '@assets/Temazcal.jpg'
	const newdata = []
	const assingImages = () => {
		serviciosData.servicio.forEach((element, index) => {
			const serviceData = {
				descripcion: element.descripcion,
				fotosWeb: '',
				titulo: element.titulo,
			}
			if (element.titulo === 'Alberca') serviceData.fotosWeb = imagenAlberca.src
			if (element.titulo === 'Gimnasio') serviceData.fotosWeb = imagenGimnasio.src
			if (element.titulo === 'Habitacion') serviceData.fotosWeb = imagenHabitacion.src
			if (element.titulo === 'Jardin') serviceData.fotosWeb = imagenJardin.src
			if (element.titulo === 'Restaurante') serviceData.fotosWeb = imagenRestaurante.src
			if (element.titulo === 'Salon') serviceData.fotosWeb = imagenSalon.src
			if (element.titulo === 'Sauna') serviceData.fotosWeb = imagenSauna.src
			if (element.titulo === 'Temazcal') serviceData.fotosWeb = imagenTemazcal.src
			newdata.push(serviceData)
		})
	}
	assingImages()
</script>

<style scoped></style>
