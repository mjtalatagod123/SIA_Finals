<template>
	<div class="app">
		<header>
			<h1><strong>Anime</strong> Search App</h1>

			<form class="search-box" @submit.prevent="HandleSearch">
				<input 
					type="search" 
					class="search-field" 
					placeholder="Search for the anime..."
					required
					v-model="search_query" />
			</form>
		</header>
		<main>
			<div class="cards" v-if="animelist.length > 0">
				<Card 
					v-for="anime in animelist" 
					:key="anime.mal_id"
					:anime="anime" />
			</div>
			<div class="no-results" v-else>
				<h3>Sorry, we have no results...</h3>
			</div>
		</main>
	</div>
</template>

<script>
import { ref } from 'vue';
import Card from './components/Card';

export default {
	setup() {
		const search_query = ref("");
		const animelist = ref([]);

		const HandleSearch = async () => {
			animelist.value = await fetch(`https://api.jikan.moe/v3/search/anime?q=${search_query.value}`)
				.then(res => res.json())
				.then(data => data.results);

			search_query.value = "";
		}

		return {
			Card,
			search_query,
			animelist,
			HandleSearch
		}
	}
}
</script>

<style lang="scss">
* {
	box-sizing: border-box;
}

header {
	padding-top: 50px;
	padding-bottom: 50px;

	h1 {
		color: gray;
		font-size: 40px;
		text-align: center;
		margin-bottom: 20px;

		strong {
			color: black;
		}
	}

	.search-box {
		display: flex;
		justify-content: center;
		padding-left: 30px;
		padding-right: 30px;

		.search-field {
			background-color: whitesmoke;
			display: block;
			width: 100%;
			max-width: 600px;
			padding: 15px;
			border-radius: 8px;
			color: darkslategrey;
			font-size: 20px;
			transition: 0.4s;
			&::placeholder {
				color: lightgray;
			}
			&:focus, &:valid {
				color: white;
				background-color: black;
			}
		}
	}
}

main {
	max-width: 1200px;
	margin: 0 auto;
	padding-left: 30px;
	padding-right: 30px;

	.cards {
		display: flex;
		flex-wrap: wrap;
		margin: 0 -8px;
	}
}
</style>
