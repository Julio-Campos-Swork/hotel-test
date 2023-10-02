<template>
	<div class="flex justify-center p-2">
		<div id="carrousel" class="relative w-full lg:w-3/4 max-w-6xl">
			<p
				class="text-center text-white text-2xl font-semibold py-2 lg:py-4 lg:pt-16 lg:text-4xl subTitleFont"
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
								? 'bg-green-400  w-3 h-3 lg:w-4 lg:h-4 rounded-full flex flex-col '
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
		<a
			:href="`/servicios/${titleDisplay}`"
			:aria-label="`Ir al servicio, ${titleDisplay}`"
		>
			<button class="botonInfo">
				Información sobre {{ titleDisplay }}
				<i class="fa fa-solid fa-arrow-right px-3 pt-1 w-[15px]"></i>
			</button>
		</a>
	</div>
</template>

<script setup>
	import { ref, onBeforeMount } from 'vue'
	const { data, timeMS, hasManyPhotos } = defineProps({
		data: Array,
		timeMS: Number,
		hasManyPhotos: Boolean,
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
		if (hasManyPhotos) {
			slider()
		}
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
