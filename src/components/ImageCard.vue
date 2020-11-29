<template>
  <transition name="fade">
    <div class="flip-card">
      <div class="flip-card-inner text-left">
        <image-card-front ref="cardFront" :image="image"></image-card-front>
        <image-card-back
            :exif-data="image.exifData"
            :id="image.id"
            @delete="deleteImage"></image-card-back>
      </div>
    </div>
  </transition>
</template>

<script>
import ImageCardFront from "@/components/ImageCardFront";
import ImageCardBack from "@/components/ImageCardBack";

export default {
  name: "ImageCard",
  components: {
    ImageCardBack,
    ImageCardFront
  },
  props: {
    image: {}
  },
  mounted() {
/*    console.log('url', URL.createObjectURL(this.image.img));
    console.log('exifdata', this.image.img);*/
  },
  methods: {
    deleteImage(id) {
      this.$emit("delete", id);
    },
    rotate(id) {
      console.log(id);
      this.$refs.cardFront.rotate(id);
    }
  }
}
</script>

<style scoped>

</style>
