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
				'https://picsum.photos/id/236/400/400',
				'https://picsum.photos/id/237/400/400',
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
			step: '',
			currentSlide: 0,
			newStep: '',
			setIndex: ''

		};
	},
	computed: {
		carouselLen() {
			let carLen = this.data.length - 1;

			return carLen;
		}
	},
	methods: {

		setStep() {
			const innerWidth = this.$refs.inner.scrollWidth;
			const totalCards = this.carouselLen + 1;
			this.step = (innerWidth / totalCards);
			console.log(this.carouselLen);
		},

		currentSlidePlus() {
			let slideChecked = this.currentSlide++;
			console.log(slideChecked);
		},

		currentSlideNext() {
			this.newStep = ((this.newStep) + (this.step) * -1);
		},

		moveNext() {
			if (this.currentSlide < (this.carouselLen - 2)) {
				this.currentSlidePlus();
				this.currentSlideNext();
				this.innerStyles = {
					transform: `translateX(${this.newStep}px)`
				};
			} else if (this.currentSlide == (this.carouselLen - 2)) {
				this.currentSlide = 0;
				this.newStep = 0;
				this.innerStyles = {
					transform: 'translateX(0px)' };
			}
		},

		currentSlideLessOne() {
			let slideChecked = this.currentSlide--;
			console.log(slideChecked);
		},


		currentSlidePrev() {
			this.newStep = ((this.newStep) - (this.step) * -1);
		},

		movePrev() {
			if (this.currentSlide > 1) {
				this.currentSlideLessOne();
				this.currentSlidePrev();
				this.innerStyles = {
					transform: `translateX(${this.newStep}px)`
				};
				console.log(this.innerStyles);
			} else if (this.currentSlide === 1) {
				this.currentSlide = 0;
				this.newStep = 0;
				this.innerStyles = {
					transform: 'translateX(0px)' };
			}
		},

		goto(index) {
			this.newStep = this.step * index * -1;
			this.currentSlide = index;
			this.innerStyles = {
				transform: `translateX(${this.newStep}px)`
			};
		}
	},
	mounted() {
		this.setStep();
		this.currentSlideNext();
		this.currentSlidePrev();
	}
};
</script>

<template>
    <div>

        <div class="slider-wrapper">
            <div class="wrapper" >
                <div class="inner" ref="inner" :style="innerStyles">
                        <div v-for='photo in data' :key="photo" class="card" >
                            <images-for-carousel :photoLink="photo" :slideNumber="photo.id"  >
                            </images-for-carousel>
                        </div>
                </div>
            </div>
            <div class="arrows">
                <arrows-for-carrusel class="left" @click="movePrev" :class="(this.currentSlide <= 0) ? 'disabled' : 'active'"/>
                <arrows-for-carrusel class="right" @click="moveNext"/>
            </div>
        </div>

        <div class="indicators">
            <div v-for='(id, index) in data' :key="id" :index="index"  :class="(this.currentSlide == index) ? 'active' : 'normal'" @click="goto(index)" class="dots">
                <dots-indicators :photoid="'photo' + id.id"/>
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
    top: 300px;
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
