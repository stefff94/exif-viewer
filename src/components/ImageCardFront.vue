
<template>
  <div class="flip-card-front">
    <div class="ui card">
      <div class="content">
        <img class="ui image"
             :id="'image-' + image.id"
             :src="image.src">
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery';

export default {
  name: "ImageCardFront",
  props: {
    image: {}
  },
  data() {
    return {
      currentRotationAngle: 0
    }
  },
  methods: {
    rotate() {
      const img = $('#image-' + this.image.id);

      this.currentRotationAngle += 90;

      img.removeClass("rotated-90")
      img.removeClass("rotated-180")
      img.removeClass("rotated-270")

      if (this.currentRotationAngle % 360 !== 0) {
        img.addClass("rotated-" + this.currentRotationAngle % 360);
      }

    }
  }
}
</script>

<style scoped>

.content {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100%;
  padding: 10px;
}

.ui.image {
  max-height: 100%
}

.rotated-180 {
  transform: rotate(180deg);
}

@media only screen and (min-width: 980px) {
  .rotated-90 {
    transform: rotate(90deg);
    max-width: 380px !important;
  }

  .rotated-270 {
    transform: rotate(270deg);
    max-width: 380px !important;
  }
}

@media only screen and (max-width: 979px) {
  .rotated-90 {
    transform: rotate(90deg);
    max-width: 350px !important;
  }

  .rotated-270 {
    transform: rotate(270deg);
    max-width: 350px !important;
  }
}

@media only screen and (max-width: 920px) {
  .rotated-90 {
    transform: rotate(90deg);
    max-width: 330px !important;
  }

  .rotated-270 {
    transform: rotate(270deg);
    max-width: 330px !important;
  }
}

@media only screen and (max-width: 860px) {
  .rotated-90 {
    transform: rotate(90deg);
    max-width: 300px !important;
  }

  .rotated-270 {
    transform: rotate(270deg);
    max-width: 300px !important;
  }
}

@media only screen and (max-width: 795px) {
  .rotated-90 {
    transform: rotate(90deg);
    max-width: 270px !important;
  }

  .rotated-270 {
    transform: rotate(270deg);
    max-width: 270px !important;
  }
}

@media only screen and (max-width: 720px) {
  .rotated-90 {
    transform: rotate(90deg);
    max-width: 240px !important;
  }

  .rotated-270 {
    transform: rotate(270deg);
    max-width: 240px !important;
  }
}

</style>
