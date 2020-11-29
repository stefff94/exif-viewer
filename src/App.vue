<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <HelloWorld msg="Welcome to Exif Viewer App"/>

    <image-input class="mt35" @upload="addImage"></image-input>

    <!-- two column stackable -->
    <div class="ui grid mt35 centered">
      <div class="eight wide widescreen eight
              wide large screen twelve wide computer
              fourteen wide tablet sixteen wide mobile column"
           v-for="image in images"
           v-bind:key="image.id">
        <div><i class="small ui button top-right" @click="rotate(image.id)">Rotate</i></div>
        <image-card :image="image" :ref="image.id" @delete="deleteImage"></image-card>
      </div>
      <!--<image-card class="eight wide widescreen eight wide large screen twelve wide computer fourteen wide tablet sixteen wide mobile column"
            v-for="image in images"
            :image="image"
            v-bind:key="image.id"
            @delete="deleteImage"
            style="margin-bottom: 20px!important;">
      </image-card>-->
    </div>
  </div>
</template>

<script>
import ExifReader from 'exifreader';

import HelloWorld from './components/HelloWorld.vue'
import ImageInput from "@/components/ImageInput";
import ImageCard from "@/components/ImageCard";

export default {
  name: 'App',
  components: {
    ImageCard,
    ImageInput,
    HelloWorld
  },
  data() {
    return {
      images: [],
      reader: FileReader,
      tmpSrc: null,
    }
  },
  mounted() {
    this.reader = new FileReader();
    this.reader.onload = (readerEvent) => {

      const tags = ExifReader.load(readerEvent.target.result);

      this.images.push({
        id: this.getImageId(),
        exifData: tags,
        src: this.tmpSrc,
      });

      this.tmpSrc = null;
    };
  },
  methods: {
    deleteImage(id) {
      this.images.splice(
          this.images.findIndex(i => i.id === id), 1);
    },
    addImage(image) {
      this.tmpSrc = URL.createObjectURL(image);

      this.reader.readAsArrayBuffer(image);
    },
    getImageId() {
      let maxImageId = -1;
      if (this.images.length > 0) {
        maxImageId = Math.max
            .apply(Math, this.images.map(i => i.id));
      }

      return maxImageId + 1;
    },
    rotate(id) {
      /*this.$emit("rotate", id); */
      console.log(this.$refs[id])
      this.$refs[id].rotate(id);
    }
  }
}
</script>

<style>

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 70%;
  margin: auto!important;
}

.top-right {
  position: absolute;
  top: -15px;
  right: 10px;
}

</style>
