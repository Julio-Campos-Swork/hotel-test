<template>
	<div class="flex justify-center p-2" data-aos="fade-up">
		<div id="carrousel" class="relative w-full lg:w-3/4 max-w-6xl">
			<p
				class="text-center text-white text-2xl font-semibold py-2 lg:pb-8 lg:pt-12 lg:text-4xl subTitleFont"
			>
				{{ titleDisplay }}
			</p>
			<div class="overflow-hidden rounded-lg h-96 lg:h-96 mt-32">
				<div :class="data.class" v-for="(data, index) in storagedData" :key="index">
					<img
						:src="data.src"
						class="absolute box block md:h-76 md:w-full lg:w-full object-cover h-96 w-96 -translate-x-1/2 -translate-y-1/2 top-1/2 left-1/2"
						:alt="data.title"
					/>
				</div>
				<!-- Slider indicators -->
				<div
					class="absolute flex flex-row space-x-3 pb-2 -translate-x-1/2 bottom-10 left-1/2"
				>
					<button
						@click="changeByButton(indexB)"
						:class="
							index === indexB
								? 'bg-[#A76BB2]  w-3 h-3 lg:w-4 lg:h-4 rounded-full flex flex-col '
								: 'w-3 h-3  lg:w-4 lg:h-4 rounded-full bg-white flex flex-col '
						"
						v-for="(data, indexB) in storagedData"
						:key="indexB"
						:aria-label="'boton' + data.title"
					></button>
				</div>
			</div>
			<!-- Slider controls -->
			<button
				aria-label="Anterior Servicio"
				type="button"
				@click="prevImage()"
				class="absolute top-72 left-8 flex items-center justify-center cursor-pointer group focus:outline-none hover:scale-110"
			>
				<i
					class="fa fa-solid fa-arrow-left inline-flex items-center justify-center w-10 h-10 rounded-full bg-white/60 hover:scale-110 group-hover:bg-white/50 dark:group-hover:bg-gray-400/60"
				></i>
			</button>
			<button
				aria-label="Siguiente Servicio"
				type="button"
				@click="nextImage()"
				class="absolute top-72 right-8 flex items-center justify-center cursor-pointer group focus:outline-none hover:scale-110"
			>
				<i
					class="fa fa-solid fa-arrow-right inline-flex items-center justify-center w-10 h-10 rounded-full bg-white/60 hover:scale-110 group-hover:bg-white/50 dark:group-hover:bg-gray-400/60"
				></i>
			</button>
		</div>
	</div>
	<div class="flex justify-center pt-2 pb-8">
		<!-- <a
			:href="`/servicios/${titleDisplay}`"
			:aria-label="`Ir al servicio, ${titleDisplay}`"
		>
			<button class="botonInfo">
				Información sobre {{ titleDisplay }}
				<i class="fa fa-solid fa-arrow-right px-3 pt-1 w-[15px]"></i>
			</button>
		</a> -->
		<a
			:aria-label="`Ir al servicio, ${titleDisplay}`"
			:href="`/servicios/${titleDisplay}`"
			class="relative inline-flex items-center justify-center p-4 px-6 py-3 overflow-hidden font-medium bg-[#A76BB2] text-indigo-600 transition duration-300 ease-out rounded-full shadow-md group"
		>
			<span
				class="absolute inset-0 flex items-center justify-center w-full h-full text-white duration-300 -translate-x-full bg-[#DB87CD] group-hover:translate-x-0 ease"
			>
				<svg
					class="w-7 h-7"
					fill="none"
					stroke="currentColor"
					viewBox="0 0 24 24"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						stroke-linecap="round"
						stroke-linejoin="round"
						stroke-width="2"
						d="M14 5l7 7m0 0l-7 7m7-7H3"
					></path>
				</svg>
			</span>
			<span
				class="absolute flex items-center justify-center w-full h-full text-white transition-all duration-300 transform group-hover:translate-x-full ease"
				>Información sobre {{ titleDisplay }}</span
			>
			<span class="relative invisible">Información sobre {{ titleDisplay }}</span>
		</a>
	</div>
</template>

<script setup>
	import { ref, onBeforeMount } from 'vue'
	const { data, timeMS } = defineProps({
		data: Array,
		timeMS: Number,
	})
	const titleDisplay = ref('')
	const storagedData = ref([])
	const index = ref(0)
	const isSliding = ref(true)
	onBeforeMount(() => {
		data.forEach((element, index) => {
			const sliderData = {
				title: element.titulo,
				src: element.fotosWeb,
				class:
					index != 0 ? ' hidden' : 'transition-opacity duration-300 ease-in opacity-100',
			}
			storagedData.value.push(sliderData)
		})
		titleDisplay.value = storagedData.value[0].title
	})

	//inicio de componente que nos permitirá hacer el sliding (en caso de decir que tiene varias imagenes)
	setInterval(() => {
		slider()
	}, timeMS)

	const slider = () => {
		if (isSliding.value) {
			nextImage(true)
		} else {
			isSliding.value = true
		}
	}
	const prevImage = (auto) => {
		if (!auto) isSliding.value = false

		if (index.value === 0) {
			storagedData.value[index.value].class =
				'transition-opacity duration-300 ease-in-out opacity-10'
			setTimeout(() => {
				storagedData.value[index.value].class = 'hidden'
				index.value = storagedData.value.length - 1
				titleDisplay.value = storagedData.value[index.value].title
				storagedData.value[index.value].class =
					'transition-opacity duration-300 ease-in opacity-100'
			}, 300)
		} else {
			storagedData.value[index.value].class =
				'transition-opacity duration-300 ease-in-out opacity-10'
			setTimeout(() => {
				storagedData.value[index.value].class = 'hidden'
				index.value--
				titleDisplay.value = storagedData.value[index.value].title
				storagedData.value[index.value].class =
					'transition-opacity duration-300 ease-in opacity-100'
			}, 300)
		}
	}
	const nextImage = (auto) => {
		if (!auto) isSliding.value = false
		if (index.value >= storagedData.value.length - 1) {
			storagedData.value[index.value].class =
				'transition-opacity duration-300 ease-in-out opacity-10'
			setTimeout(() => {
				storagedData.value[index.value].class = 'hidden'
				index.value = 0
				titleDisplay.value = storagedData.value[index.value].title
				storagedData.value[index.value].class =
					'transition-opacity duration-300 ease-in opacity-100'
			}, 300)
		} else {
			storagedData.value[index.value].class =
				'transition-opacity duration-300 ease-in-out opacity-10'
			setTimeout(() => {
				storagedData.value[index.value].class = 'hidden'
				index.value++
				titleDisplay.value = storagedData.value[index.value].title
				storagedData.value[index.value].class =
					'transition-opacity duration-300 ease-in opacity-100'
			}, 300)
		}
	}

	const changeByButton = (indexB) => {
		isSliding.value = false
		storagedData.value[index.value].class =
			'transition-opacity duration-300 ease-in-out opacity-10'
		setTimeout(() => {
			storagedData.value[index.value].class = 'hidden'

			titleDisplay.value = storagedData.value[indexB].title
			storagedData.value[indexB].class =
				'transition-opacity duration-300 ease-in-out opacity-100'
			index.value = indexB
		}, 300)
	}
</script>
