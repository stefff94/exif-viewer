<template>
  <div id="app">
    <!--<img alt="Vue logo" src="./assets/logo.png">-->
    <HelloWorld msg="Welcome to Exif Viewer App"/>

    <image-input class="mt35" @upload="addImage"></image-input>

    <!-- two column stackable -->
    <div class="ui grid mt35 centered">
      <div class="eight wide widescreen eight wide large screen twelve wide computer fourteen wide tablet sixteen wide mobile column" v-for="image in images" v-bind:key="image.id">
        <image-card :image="image" @delete="deleteImage"></image-card>
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
      images: []
      /*images: [{id:1, data: null}, {id:2, data: null}, {id:3, data:null}]*/
    }
  },
  methods: {
    deleteImage(id) {
      this.images.splice(
          this.images.findIndex(i => i.id === id), 1);
    },
    addImage(imageSrc) {
      let maxImageId = 0;
      if(this.images.length > 0)
        maxImageId = Math.max
            .apply(Math, this.images.map(i => i.id));

      let image = {
        id: maxImageId + 1,
        src: imageSrc
      }
      this.images.push(image);
    }
  }
}
</script>

<style>
/*#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}*/
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  width: 70%;
  margin: auto!important;
}
</style>
