<template>
  <transition name="fade">
    <div class="flip-card">
      <div class="flip-card-inner text-left">
        <image-card-front
            :image="image">

        </image-card-front>
        <image-card-back
            :exif-data="image.exifData"
            :id="image.id"
            @delete="deleteImage">

        </image-card-back>
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
  methods: {
    deleteImage(id) {
      this.$emit("delete", id);
    },
    rotate() {
      this.$children[0].rotate();
    }
  }
}
</script>

<style scoped>

</style>
