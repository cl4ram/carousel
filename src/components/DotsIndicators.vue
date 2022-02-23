<script>
export default {
	name: 'DotsIndicators',
	props: {
		photoid: String
	}
};
</script>

<template>

        <div :class="photoid" ></div>

</template>

<style scoped>
    div{
        width: 10px;
        height: 10px;
        border-radius: 50px;
        background-color: #242424;
        margin: 5px;
        cursor: pointer;
        opacity: 50%;
    }

    div:hover{
        opacity: 100%;
    }

</style>
