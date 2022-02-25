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
                <arrows-for-carrusel class="left" @click="changePosition(-1)" :class="(this.currentSlide <= 0) ? 'disabled' : 'active'"/>
                <arrows-for-carrusel class="right" @click="changePosition(1)"/>
            </div>
        </div>

        <div class="indicators">
            <div v-for='(id, index) in data' :key="id" :class="(this.currentSlide == index) ? 'active' : 'normal'" class="dots">
                <dots-indicators :data-number="index" @dotClick="changePosition" :index="index"  />
            </div>
        </div>

    </div>
</template>

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
			step: null,
			currentSlide: 0


		};
	},
	methods: {
		setStep() {
			this.step = (this.$refs.inner.scrollWidth / (this.data.length));
		},

		changePosition(variable) {
			if (Number.isInteger(variable)) {
				this.setMove(variable);
			} else {
				this.goto();
			}
		},
		setMove(direction) {
			this.currentSlide += direction;
			this.innerStyles = {
				transform: `translateX(-${this.currentSlide * this.step}px)`
			};
		},
		goto() {
			this.currentSlide = Number(event.target.dataset.number);
			this.innerStyles = {
				transform: `translateX(-${this.currentSlide * this.step}px)`
			};
		}
	},
	watch: {
		currentSlide() {
			if ((this.currentSlide == this.data.length - 2) || this.currentSlide < 1) {
				this.currentSlide = 0;
				this.innerStyles = {
					transform: 'translateX(0px)'
				};
			}
		}
	},
	mounted() {
		this.setStep();
	}
};
</script>

<style>

h1 {
    background-color: rgb(85, 85, 85);
    color: white;
    text-align: center;
    font-family: 'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}

.slider-wrapper {
    position: relative;
    display: flex;
    overflow: hidden;
    justify-content: center;
    width: 100%;
}

.wrapper {
    overflow: hidden;
    width: calc(400px * 3);
}

.inner {
    white-space: nowrap;
    transition: transform 0.5s;
}

.card {
    display: inline-flex;
    width: 400px;
    margin-right: 10px;
}

.arrows {
    position: absolute;
    top: 200px;
    display: flex;
    width: 100%;
}

.disabled .arrow {
    opacity: 10%;
    cursor: auto;
}

.disabled .arrow:hover {
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

.indicators .active div {
    background-color: #ff0000;
}

.indicators {
    display: flex;
    justify-content: center;
    margin-top: 20px;
}

.dots:last-child,
.dots:nth-last-child(2) {
    display: none;
}


</style>
