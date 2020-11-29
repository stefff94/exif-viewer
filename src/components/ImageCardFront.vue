
<template @rotate="rotate">
  <div class="flip-card-front">
    <div class="ui card">
      <div class="content" style="padding: 10px">
        <img class="ui image" :src="image.src" style="max-height: 380px; height: 38vw;">
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
      fixedHeight: true
    }
  },
  methods: {
    rotate(id) {
      console.log(id);

      const img = $('.ui.image');
      const width = img.width();
      const height = img.height();

      if (this.fixedHeight) {
        img.css("height", "");
      } else {
        img.css("width", "");
      }
      this.fixedHeight = !this.fixedHeight;

      if (this.fixedHeight) {
        img.css("height", width + "px");
      } else {
        img.css("width", height + "px");
      }


      /*img.width(height + 'px');
      img.height(width + 'px');*/
      img.addClass("rotated");
    },
    rotate2() {
      const img = $('.ui.image');
      img.addClass("rotated");
      img.width("500px");
    }
  }
}
</script>

<style scoped>

.content {
  display: flex;
  align-items: center;
  justify-content: center;
}

.rotated {
  transform: rotate(90deg);
}

</style>
