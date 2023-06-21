<template>
  <div class="wrapper">
    <div class="item" :class="{'rotate-right': index % 2 === 0, 'rotate-left': index % 2 === 1}">
      <div class="polaroid">
        <img :src="image.src">
        <div class="caption my-cursive">{{ image.caption }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Polaroid',
  props: {
    image: {
      type: Object, // ensure image is an object
      required: true, // image prop is required
      validator: function (value) { // this function validates the structure of the image object
        return value && typeof value.src === 'string' && typeof value.caption === 'string'
      }
    },
    index: {
      type: Number, // ensure index is a number
      required: true
    }
  }
})
</script>

<style>
* { box-sizing: border-box }

.wrapper {
  width: 100%;
  padding: 0 1rem;
  text-align: left;
}

.polaroid {
  background: #fff;
  padding: 1rem;
  box-shadow: 0 0.2rem 1.2rem rgba(0,0,0,0.2);
}

.polaroid > img {
  max-width: 100%;
  height: auto;
}

.caption {
  font-size: 1.8rem;
  text-align: center;
  line-height: 2em;
  color: black;
}

.item {
  display: inline-block;
  margin-top: 1rem;
  filter: grayscale(100%);
}

.item .polaroid::before {
  content: '';
  position: absolute;
  z-index: -1;
  transition: all 0.35s;
}

.item:hover {
  filter: none;
  transform: scale(1, 1) rotate(0deg) !important;
  transition: all 0.35s;
}

.item:hover .polaroid::before {
  content: '';
  position: absolute;
  z-index: -1;
  transform: rotate(0deg);
  height: 90%;
  width: 90%;
  bottom: 0%;
  right: 5%;
  box-shadow: 0 1rem 3rem rgba(0,0,0,0.2);
  transition: all 0.35s;
}

.rotate-right {
  transform: scale(0.8, 0.8) rotate(5deg);
  transition: all 0.35s;
}

.rotate-left {
  transform: scale(0.8, 0.8) rotate(-5deg);
  transition: all 0.35s;
}

@media (max-width: 600px) {
  .item {
    width: 100%;
    display: block;
    margin: 2rem auto;
  }

  .polaroid { padding: 1rem }
}
</style>
