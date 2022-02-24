<script>
export default {
	name: 'ImagesForCarousel'
};
</script>

<template>
    <div>
        <div class="arrow"></div>
    </div>
</template>

<style scoped>
    .arrow {
        border: solid #f80000;
        border-width: 0 6px 6px 0;
        display: inline-block;
        padding: 6px;
        cursor: pointer;
        opacity: 50%;
    }

    .arrow:hover{
        opacity: 100%;
    }

</style>
