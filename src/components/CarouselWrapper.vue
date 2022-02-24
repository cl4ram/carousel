<script>
import ImagesForCarousel from './ImagesForCarousel.vue';
import DotsIndicators from './DotsIndicators.vue';
import ArrowsForCarrusel from './ArrowsForCarrusel.vue';

export default {
	name: 'CarouselWrapper',
	components: { ImagesForCarousel, DotsIndicators, ArrowsForCarrusel },
	data() {
		return {
			data: ['https://picsum.photos/id/237/400/400',
				'https://picsum.photos/id/238/400/400',
				'https://picsum.photos/id/239/400/400',
				'https://picsum.photos/id/240/400/400',
				'https://picsum.photos/id/241/400/400',
				'https://picsum.photos/id/242/400/400',
				'https://picsum.photos/id/243/400/400',
				'https://picsum.photos/id/244/400/400',
				'https://picsum.photos/id/235/400/400',
				'https://picsum.photos/id/236/400/400'],
			innerStyles: {},
			currentSlide: 0,
			step: '',
			afterMoveStep: 0

		};
	},
	computed: {
		carouselLength() {
			let carouselLength = this.data.length;

			return carouselLength;
		}
	},
	methods: {

		setStep() {
			this.step = (this.$refs.inner.scrollWidth / (this.carouselLength));
		},

		move(moveStep) {
			this.currentSlide = this.currentSlide + moveStep;
			if (moveStep >= 0) {
				console.log(this.currentSlide);
				this.afterMoveStep = ((this.afterMoveStep) + (this.step) * -1);
				console.log(this.afterMoveStep);
				this.innerStyles = {
					transform: `translateX(${this.afterMoveStep}px)`
				};
			} else if ((this.currentSlide == this.carouselLength - 2) || (this.currentSlide < 1)) {
				this.currentSlide = 0;
				this.afterMoveStep = 0;
				this.innerStyles = {
					transform: 'translateX(0px)' };
			} else {
				this.afterMoveStep = ((this.afterMoveStep) - (this.step) * -1);
				this.innerStyles = {
					transform: `translateX(${this.afterMoveStep}px)`
				};
			}

			if ((this.currentSlide == this.carouselLength - 2) || (this.currentSlide < 1)) {
				this.currentSlide = 0;
				this.afterMoveStep = 0;
				this.innerStyles = {
					transform: 'translateX(0px)' };
			}
		},


		goto(index) {
			this.afterMoveStep = this.step * index * -1;
			this.currentSlide = index;
			this.innerStyles = {
				transform: `translateX(${this.afterMoveStep}px)`
			};
		}
	},
	mounted() {
		this.setStep();
	}
};
</script>

<template>
    <div>

        <div class="slider-wrapper">
            <div class="wrapper" >
                <div class="inner" ref="inner" :style="innerStyles">
                        <div v-for='photo in data' :key="photo" class="card" >
                            <images-for-carousel :photoLink="photo">
                            </images-for-carousel>
                        </div>
                </div>
            </div>
            <div class="arrows">
                <arrows-for-carrusel class="left" @click="move(-1)" :class="(this.currentSlide <= 0) ? 'disabled' : 'active'"/>
                <arrows-for-carrusel class="right" @click="move(1)"/>
            </div>
        </div>

        <div class="indicators">
            <div v-for='(id, index) in data' :key="id" :class="(this.currentSlide == index) ? 'active' : 'normal'" class="dots">
                <dots-indicators :photoid="'photo' + id.id" @goto="goto" :index="index"  />
            </div>
        </div>

    </div>
</template>

<style>

h1 {
    color: white;
    background-color: rgb(85, 85, 85);
    text-align: center;
    font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

.slider-wrapper{
    width: 100%;
    overflow: hidden;
    display: flex;
    justify-content: center;
	position: relative;
}

.wrapper{
    width: calc(400px * 3);
    overflow: hidden;
}

.inner{
  transition: transform .5s;
  white-space: nowrap;
}
.card {
  margin-right: 10px;
  display: inline-flex;
  width: 400px;
}

.arrows {
    position: absolute;
    top: 200px;
    display: flex;
    width: 100%;
}

.disabled .arrow{
    opacity: 10%;
    cursor: auto;
}

.disabled .arrow:hover{
    opacity: 10%;
}


.left {
    position: absolute;
    left: 2%;
}

.left .arrow {
    transform: rotate(135deg);
}

.right {
    position: absolute;
    right: 2%;
}

.right .arrow {
    transform: rotate(-45deg);
}

.indicators .active div{
	background-color: #ff0000;
}

.indicators{
    display: flex;
    justify-content: center;
    margin-top: 20px;
}

.dots:last-child,
.dots:nth-last-child(2){
	display: none;
}

</style>
