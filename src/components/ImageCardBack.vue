
<template>
  <div class="flip-card-back">
    <div class="ui card">
      <div class="content">
        <i class="right floated large icon trash alternate outline delete"
           @click="deleteImage"></i>
        <div class="header text-center">Exif Data</div>
        <div class="description mt30">
          <div class="ui bulleted list">
            <div class="item"
                 v-for="data in exifData"
                 v-bind:key="data.id">

              {{ data.name }} | {{ data.value }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ImageCardBack",
  props: {
    exifData: Array,
    id: Number
  },
  methods: {
    deleteImage() {
      this.$emit("delete", this.id);
    }
  }
}
</script>

<style scoped>

</style>
