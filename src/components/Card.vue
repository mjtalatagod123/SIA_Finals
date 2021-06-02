<template>
	<div class="card">
		<a :href="anime.url" target="_blank">
			<img 
				:src="anime.image_url" 
				:alt="anime.title + ' Poster'" 
			/>
			<h3>{{ anime.title }}</h3>
		</a>
	</div>
</template>

<script>
export default {
	props: ['anime']
}
</script>

<style lang="scss" scoped>
.card {
	flex: 1 1 33%;
	width: 33%;
	max-width: 33%;
	padding: 0px 8px;
	margin-bottom: 16px;

	img {
		width: 100%;
		height: 300px;
		object-fit: cover;
		border-radius: 16px;
	}

	h3 {
		padding: 16px;
		color: black;
	}

	&:hover {
		img {
			transform: scale(1.05);
		}
		h3 {
			color: red;
		}
	}
}
</style>