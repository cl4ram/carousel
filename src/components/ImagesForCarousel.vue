<script>
export default {
	name: 'ImagesForCarousel',
	props: {
		photoLink: {
			type: String,
			required: true
		}
	}

};
</script>

<template>
    <div class="slide">
        <img :src="photoLink" />
    </div>
</template>

<style scoped>

img{
	width: 300px;
	height: 300px;
}

</style>
