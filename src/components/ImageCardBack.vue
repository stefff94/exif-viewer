
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
                   v-for="data in previewExifDataMap"
                   v-bind:key="data.id">

                <strong>{{ data[0] }}</strong> - <span>{{ data[1] }}</span>
              </div>
            </div>
          </div>
          <div class="bottom-right">
            <div class="ui black button"
               v-if="mayViewMoreData"
               @click="showAll()">

              All data
            </div>
            <a v-if="hasGPSGeolocation"
               class="not-mobile ui green icon button"
               :href="'https://www.google.com/maps/search/?api=1&query=' + this.exifDataMap.get('GPSLatitude') + ',' + this.exifDataMap.get('GPSLongitude')"
               target="_blank">

              <i class="map marker alternate icon"></i>
            </a>
          </div>
        </div>
      </div>
    </div>
    <div class="ui modal" :id="'modal-' + id">
      <i class="close icon"></i>
      <div class="header">
        Exif Data Viewer
      </div>
      <div class="content">
        <div class="description">
          <div class="ui bulleted list">
            <div class="item"
                 v-for="data in exifDataMap"
                 v-bind:key="data.id">

              <strong>{{ data[0] }}</strong> - {{ data[1] }}
            </div>
          </div>
        </div>
      </div>
      <div class="actions">
        <div class="ui black deny button">
          Close
        </div>
        <a v-if="hasGPSGeolocation"
           class="ui green right labeled icon button"
           :href="'https://www.google.com/maps/search/?api=1&query=' + this.exifDataMap.get('GPSLatitude') + ',' + this.exifDataMap.get('GPSLongitude')"
           target="_blank">

          See in Google Maps
          <i class="map marker alternate icon"></i>
        </a>
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
      previewExifData: [],
      exifDataMap: null,
      previewExifDataMap: null
    }
  },
  mounted() {
    // set the exifDataMap Object
    this.exifDataMap = new Map();

    Object.entries(this.exifData)
        .filter(d => d[1].description !== undefined && d[1].description !== "")
        .forEach(d => this.exifDataMap.set(d[0], d[1].description))

    // set the previewExifDataMap Object
    this.previewExifDataMap = new Map();

    Array.from(this.exifDataMap.entries())
        .slice(0, 6)
        .forEach(d => this.previewExifDataMap.set(d[0], d[1]))
  },
  computed: {
    mayViewMoreData() {
      let exifDataMapSize;
      let previewExifDataMapSize;
      if (this.exifDataMap !== null && this.previewExifDataMap !== null) {
        exifDataMapSize = this.exifDataMap.size;
        previewExifDataMapSize = this.previewExifDataMap.size;
      }

      return exifDataMapSize !== undefined
          && previewExifDataMapSize !== undefined
          && exifDataMapSize > previewExifDataMapSize;
    },
    hasGPSGeolocation() {
      let GPSLatitude;
      let GPSLongitude;
      if (this.exifDataMap !== null) {
        GPSLatitude = this.exifDataMap.get("GPSLatitude");
        GPSLongitude = this.exifDataMap.get("GPSLongitude")
      }

      return GPSLatitude !== undefined && GPSLongitude !== undefined;
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

@media only screen and (max-width: 600px) {

  .not-mobile {
    display: none !important;
  }

}

</style>
