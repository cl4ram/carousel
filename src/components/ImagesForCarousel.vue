<script>
export default {
	name: 'ImagesForCarousel',
	props:
	{
		photoLink: {
			type: String,
			required: true },
		slideNumber: Number	}

};
</script>

<template>
    <div class="slide">
        <img :src="photoLink" />
        <p>{{ slideNumber }}</p>
    </div>
</template>

<style scoped>


p {
    position: absolute;
	top: 40%;
    left: 0;
	right: 0;
	display: flex;
	justify-content: center;
    color: aliceblue;
    font: 900 56px Helvetica;
}

</style>
