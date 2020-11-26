
<template>
  <div class="flip-card-front">
    <div class="ui card">
      <div class="content" style="padding: 10px">
        <img class="ui image" :src="image.src" style="max-height: 380px; height: 38vw;">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ImageCardFront",
  props: {
    image: {}
  }
}
</script>

<style scoped>

.content {
  display: flex;
  align-items: center;
  justify-content: center;
}

</style>
