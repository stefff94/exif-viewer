<template>
  <div class="text container">
    <div class="upload-container" @drag.stop.prevent=""
         @dragover.stop.prevent=""
         @dragstart.stop.prevent=""
         @dragend.stop.prevent=""
         @dragenter.stop.prevent="onDragEnter"
         @dragleave.stop.prevent="onDragLeave"
         @drop.stop.prevent="onFileDrop"
         @click.prevent="onClick"
         v-bind:class="draggingOver ? 'dragover' : ''">

      <div class="input-text">
        <svg class="icon" xmlns="http://www.w3.org/2000/svg" width="50" height="43" viewBox="0 0 50 43">
          <path
              d="M48.4 26.5c-.9 0-1.7.7-1.7 1.7v11.6h-43.3v-11.6c0-.9-.7-1.7-1.7-1.7s-1.7.7-1.7 1.7v13.2c0
              .9.7 1.7 1.7 1.7h46.7c.9 0 1.7-.7 1.7-1.7v-13.2c0-1-.7-1.7-1.7-1.7zm-24.5 6.1c.3.3.8.5 1.2.5.4 0
              .9-.2 1.2-.5l10-11.6c.7-.7.7-1.7 0-2.4s-1.7-.7-2.4 0l-7.1 8.3v-25.3c0-.9-.7-1.7-1.7-1.7s-1.7.7-1.7
              1.7v25.3l-7.1-8.3c-.7-.7-1.7-.7-2.4 0s-.7 1.7 0 2.4l10 11.6z">
          </path>
        </svg>
        <span><strong>Choose a file</strong> or drag it here</span>
      </div>
    </div>
    <input ref="fileInput" type="file" name="fileInput" accept="image/jpeg" @change="onFileChange" />
  </div>
</template>

<script>
export default {
  name: "ImageInput",
  data() {
    return {
      draggingOver: false
    }
  },
  methods: {
    onDragEnter() {
      this.draggingOver = true;
    },
    onDragLeave() {
      this.draggingOver = false;
    },
    onFileDrop(e) {
      this.draggingOver = false;
      this.onFileChange(e);
    },
    onFileChange(e) {
      let files = e.target.files || e.dataTransfer.files

      this.$emit("upload", files[0]);
    },
    onClick() {
      this.$refs.fileInput.click();
    }
  }
}
</script>

<style scoped>

.upload-container {
  width: 100%;
  max-width: 680px;
  height: 50vw;
  max-height: 400px;
  background-color: #c8dadf;
  font-size: 1.25rem;
  outline: 2px dashed #92b0b3;
  outline-offset: -10px;
  -webkit-transition: outline-offset .15s ease-in-out, background-color .15s linear;
  transition: outline-offset .15s ease-in-out, background-color .15s linear;
  display: flex;
  align-items: center;
  justify-content: center;
  margin: 0 auto;
  cursor: pointer;
}

.input-text {
  position: relative;
  pointer-events: none;
}

.icon {
  width: 100%;
  height: 80px;
  fill: #92b0b3;
  display: block;
  margin-bottom: 40px;
}

.dragover {
  outline-offset: -20px;
  outline-color: #c8dadf;
  background-color: #fff;
}

input[type=file] {
  display: none;
}

</style>
