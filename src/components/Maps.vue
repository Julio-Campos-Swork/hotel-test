<template>
	<h4 class="text-center text-2xl lg:text-4xl text-white py-2 subTitleFont uppercase">
		Lugares turisticos y de interés
	</h4>
	<div
		class="lg:pb-2 lg:pt-10 lg:grid lg:grid-rows-1 lg:grid-flow-col flex flex-col"
		data-aos="fade-up"
	>
		<!-- lista de botones -->
		<div class="px-4">
			<div
				class="flex flex-col items-center py-1 px-1 lg:py-1 h-[250px] lg:h-[600px] lg:px-4 lg:w-full overflow-y-auto"
			>
				<button
					:id="index + ' ' + item.name"
					class="py-8 h-1/4 w-full lg:w-3/4 my-1 btn"
					v-for="(item, index) in interestPlaces"
					:key="index"
					@click="changeMap(item)"
				>
					{{ item.name }}
				</button>
			</div>
		</div>
		<!-- mapa lado derecho -->
		<div class="px-4">
			<div class="box">
				<iframe
					title="Puntos de interes"
					class="w-full h-[600px]"
					:src="activeMap"
					style="border: 0"
					allowfullscreen=""
					loading="lazy"
					referrerpolicy="no-referrer-when-downgrade"
				></iframe>
			</div>
		</div>
	</div>
</template>

<script setup>
	import { ref } from 'vue'
	const activeMap = ref(
		'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1881.4507684774749!2d-98.15327590364294!3d19.416659816382353!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d020391ee7bd35%3A0x1046f1c8d6b4f150!2sHotel%20Del%20%C3%81ngel!5e0!3m2!1sen!2smx!4v1696374332123!5m2!1sen!2smx'
	)

	const interestPlaces = [
		{
			name: 'Hotel del Ángel',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1881.4507684774749!2d-98.15327590364294!3d19.416659816382353!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d020391ee7bd35%3A0x1046f1c8d6b4f150!2sHotel%20Del%20%C3%81ngel!5e0!3m2!1sen!2smx!4v1696374332123!5m2!1sen!2smx',
		},
		{
			name: 'Maquinita',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d870.9854134489343!2d-98.14586361691588!3d19.418227226869117!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d0203b28978319%3A0xd61ae2542cfca043!2sLa%20Maquinita!5e0!3m2!1sen!2smx!4v1696370491375!5m2!1sen!2smx',
		},
		{
			name: 'Catedral',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d870.9990583426413!2d-98.14111213852502!3d19.415680784259422!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d02023f5676737%3A0x4f3445bf14b2ac5!2sBas%C3%ADlica%20De%20Nuestra%20Se%C3%B1ora%20Misericordia!5e0!3m2!1sen!2smx!4v1696374448889!5m2!1sen!2smx',
		},
		{
			name: 'Plaza Apizaco',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1507.799944942111!2d-98.13341113197555!3d19.411705826874755!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d01f8a97c23a11%3A0xca9b5ccfac359833!2sPlaza%20Apizaco!5e0!3m2!1sen!2smx!4v1696374380381!5m2!1sen!2smx',
		},
		{
			name: 'Cinepolis',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1810.434403515091!2d-98.13226508038946!3d19.411482057093625!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d01f8a97a2cc53%3A0xb73bbc19647d921!2sCin%C3%A9polis%20Apizaco!5e0!3m2!1sen!2smx!4v1696374414574!5m2!1sen!2smx',
		},
		{
			name: 'Cinepolis',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1810.434403515091!2d-98.13226508038946!3d19.411482057093625!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d01f8a97a2cc53%3A0xb73bbc19647d921!2sCin%C3%A9polis%20Apizaco!5e0!3m2!1sen!2smx!4v1696374414574!5m2!1sen!2smx',
		},
		{
			name: 'Cinepolis',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1810.434403515091!2d-98.13226508038946!3d19.411482057093625!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d01f8a97a2cc53%3A0xb73bbc19647d921!2sCin%C3%A9polis%20Apizaco!5e0!3m2!1sen!2smx!4v1696374414574!5m2!1sen!2smx',
		},
		{
			name: 'Cinepolis',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1810.434403515091!2d-98.13226508038946!3d19.411482057093625!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d01f8a97a2cc53%3A0xb73bbc19647d921!2sCin%C3%A9polis%20Apizaco!5e0!3m2!1sen!2smx!4v1696374414574!5m2!1sen!2smx',
		},
		{
			name: 'Cinepolis',
			src:
				'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d1810.434403515091!2d-98.13226508038946!3d19.411482057093625!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x85d01f8a97a2cc53%3A0xb73bbc19647d921!2sCin%C3%A9polis%20Apizaco!5e0!3m2!1sen!2smx!4v1696374414574!5m2!1sen!2smx',
		},
	]

	const changeMap = (item) => {
		activeMap.value = item.src
	}
</script>

<style scoped>
	button {
		/* padding: 10px 10px; */
		text-transform: uppercase;
		border-radius: 8px;
		/* font-size: 17px;
		font-weight: 500; */
		color: #fffffff7;
		text-shadow: none;
		background: transparent;
		box-shadow: transparent;
		border: 1px solid #ffffff80;
		transition: 0.5s ease;
		user-select: none;
	}

	.btn:hover,
	:focus {
		color: #ffffff;
		background: #008cff80;
		border: 1px solid #008cff37;
		text-shadow: 0 0 5px #0a0000, 0 0 10px #080808, 0 0 20px #ffffff;
		box-shadow: 0 0 5px #008cff, 0 0 20px #008cff, 0 0 50px #008cff, 0 0 100px #008cff;
	}

	::-webkit-scrollbar {
		width: 0.4rem; /* Ancho de la barra de desplazamiento */
		background-color: #f1f1f1; /* Color de fondo de la barra de desplazamiento */
	}

	/* Estilo para el "thumb" (el control deslizante) de la barra de desplazamiento */
	::-webkit-scrollbar-thumb {
		background-color: #2d8cc3; /* Color del control deslizante */
		border-radius: 5px; /* Borde redondeado del control deslizante */
	}

	/* Estilo para el "thumb" al pasar el ratón por encima */
	::-webkit-scrollbar-thumb:hover {
		background-color: #1a48b3; /* Color del control deslizante al pasar el ratón por encima */
	}
</style>
