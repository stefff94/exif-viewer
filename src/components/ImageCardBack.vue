
<template>
  <div>
    <div class="flip-card-back">

      <div class="ui card">
        <div class="content">
          <i class="right floated large icon trash alternate outline delete"
             @click="deleteImage"></i>
          <div class="header text-center">Exif Data</div>
          <div class="description mt30">
            <div class="ui bulleted list">
              <div class="item"
                   v-for="data in previewExifData"
                   v-bind:key="data.id">

                <strong>{{ data.property }}</strong> - <span>{{ data.value }}</span>
              </div>
            </div>
          </div>
          <div class="my-class">
            <i class="small ui button bottom-right"
               v-if="mayViewMoreData"
               @click="showAll()">

              View all
            </i>
          </div>
        </div>
      </div>
    </div>
    <div class="ui modal" v-bind:id="'modal-' + id">
      <i class="close icon"></i>
      <div class="header">
        Exif Data Viewer
      </div>
      <div class="content">
        <div class="description">
          <div class="ui bulleted list">
            <div class="item"
                 v-for="data in parsedExifData"
                 v-bind:key="data.id">

              <strong>{{ data.property }}</strong> - {{ data.value }}
            </div>
          </div>
        </div>
      </div>
      <div class="actions">
        <div class="ui black deny button">
          Close
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery';

export default {
  name: "ImageCardBack",
  props: {
    exifData: Object,
    id: Number
  },
  data() {
    return {
      parsedExifData: [],
      previewExifData: []
    }
  },
  mounted() {
    this.parsedExifData = Object.entries(this.exifData)
        .filter(o => o[1].description !== undefined && o[1].description !== "")
        .map(o => ({"property": o[0], "value": o[1].description}))

    this.previewExifData = this.parsedExifData.slice(0, 8);
  },
  computed: {
    mayViewMoreData() {
      return this.parsedExifData.length > this.previewExifData.length;
    }
  },
  methods: {
    deleteImage() {
      this.$emit("delete", this.id);
    },
    showAll() {
      $('#modal-' + this.id).modal('show');
    }
  }
}
</script>

<style scoped>

.bottom-right {
  position: absolute;
  bottom: 10px;
  right: 10px;
}

</style>
