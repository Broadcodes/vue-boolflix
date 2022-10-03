<template>
  <div>
    <div class="container">
      <div class="slider-wrapper" tabindex="0">
        <div class="item">
          <img :mouseleave="play()" :src="slides[indexItem].image" :alt="slides[indexItem].title" />
          <div class="livelEffect">
            <div class="text">
              <h3>{{slides[indexItem].title}}</h3>
              <p>
                {{slides[indexItem].text}}
              </p>
            </div>
          </div>
        </div>

        <div class="thumbs">
          <div class="thumbsContainer" v-for="(element, index) in slides" :key="index">
            <div class="thumb" v-if="slides[indexItem] === element">
              <img class="active" :src="element.image" :alt="element.title" />
            </div>
            <div class="thumb" v-else>
              <img @click="activeSlide(slides.indexOf(element))" :src="element.image" :alt="element.title" />
            </div>
          </div>
        </div>

        <div class="shadowMirror">
          <div class="thumbsMirror">
            <div class="thumbsContainer" v-for="(element, index) in slides" :key="index">
              <div class="thumbMirror" v-if="slides[indexItem] === element">
                <img class="activeMirror" :src="element.image" :alt="element.title" />
              </div>
              <div class="thumbMirror" v-else>
                <img :src="element.image" :alt="element.title" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { image } from '@/imageJumbo'

export default {
  data() {
    return {
      indexItem: 0,
      interval: '',
      slides: image
    }
  },
  methods: {
    nextSlide() {
      clearInterval(this.interval);
      this.indexItem++;
      if (this.indexItem === this.slides.length) {
        this.indexItem = 0;
      }
    },
    previousSlide() {
      clearInterval(this.interval);
      this.indexItem--;
      if (this.indexItem === - 1) {
        this.indexItem = this.slides.length - 1;
      }
    },
    // al click su una thumb, visualizzare in grande l'immagine corrispondente
    activeSlide(index) {
      clearInterval(this.interval);
      this.indexItem = index;
    },

    // applicare l'autoplay allo slider: ogni 3 secondi, cambia immagine automaticamente
    play() {
      this.interval = setTimeout(() => {
        this.interval = clearInterval(this.interval);
        this.nextSlide();
      }, 3000)
    }
  }
}
</script>

<style lang="scss" scoped>
.container {
  margin-bottom: 20px;
  box-shadow: 0px 10px 20px #000;

  .item {
    width: 100%;
    height: 450px;
    position: relative;

    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      object-position: center 12%;
      transform: scaleX(-1);
    }

    .livelEffect {
      position: absolute;
      top: 0;
      width: 100%;
      height: 100%;
      background: rgb(0, 0, 0);
      background: linear-gradient(90deg, rgb(0, 0, 0) 10%, rgba(0, 0, 0, 0) 100%);

      .text {
        position: absolute;
        width: 30%;
        top: 50%;
        transform: translateY(-50%);
        left: 70px;
        text-align: left;
        color: #fff;
        line-height: 1.9rem;
        font-size: 1.2rem;
      }

      .text h3 {
        font-size: 2.5rem;
        margin-bottom: 30px;
        line-height: 3.5rem;
      }
    }
  }

  .thumbs {
    display: flex;
    width: 100%;
    background: #000;
    position: relative;
    top: 0px;
    height: 150px;
    box-shadow: 0px 0px 100px #000;
    padding-top: 20px;
  }

  .thumbsContainer {
    margin: 0 15px;
    width: calc(100% / 5 - 30px);
  }

  .thumb {
    height: 100%;
  }

  .thumb img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    opacity: 0.5;
    cursor: pointer;
    transform: scaleX(-1);
  }

  .active {
    border: 2px solid #ccc;
    opacity: 1 !important;
  }

  .shadowMirror {
    box-shadow: inset 0px 30px 80px rgba(255, 255, 255, 0.127);
    background: #000;
    padding-bottom: 40px;

    .thumbsMirror {
      display: flex;
      width: 100%;
      position: relative;
      top: 0px;
      left: -7px;
      height: 80px;
    }

    .thumbMirror {
      height: 100%;
      transform: rotate(180deg);
    }

    .thumbMirror img {
      width: 100%;
      height: 100%;
      object-fit: cover;
      opacity: 0.15;
      transform: skew(-10deg);
    }

    .activeMirror {
      border: 2px solid rgb(138, 138, 138);
      opacity: 0.3 !important;
    }
  }
}
</style>