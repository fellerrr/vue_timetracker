<script setup>
	import TheHeader from './components/TheHeader.vue'
	import TheNav from './components/TheNav.vue'

	import TheActivities from './pages/TheActivities.vue';
	import TheTimeLine from './pages/TheTimeLine.vue';
	import TheProgress from './pages/TheProgress.vue';

	import { ref } from 'vue';
	import { normalizeHashPage } from './utils'
	import { PAGE_ACTIVITIES, PAGE_PROGRESS, PAGE_TIMELINE } from './constants';

	const currentPage = ref(normalizeHashPage())

	function goTo(page) {
		currentPage.value = page
	}
</script>

<template>
	<TheHeader 
		@go-to-time-line="goTo(PAGE_TIMELINE)"
		@go-to-progress="goTo(PAGE_PROGRESS)"
	/>

	<main class="flex flex-grow flex-col">
		<TheTimeLine v-show="currentPage === PAGE_TIMELINE"/>
		<TheActivities v-show="currentPage === PAGE_ACTIVITIES"/>
		<TheProgress v-show="currentPage === PAGE_PROGRESS"/>
	</main>

	<TheNav :current-page = "currentPage" @navigate="goTo($event)"/>	
</template>
