<template>
  <div class="GalleryImageViewer" @click="handleClose()">
    <img class="GalleryImageViewerImage" :src="src" />
  </div>
</template>
<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options<GalleryImageViewer>({
  props: {
    imgurId: String,
  },
})
export default class GalleryImageViewer extends Vue {
  public imgurId!: string;

  public get src() {
    return `https://i.imgur.com/${this.$route.params.imgurId}.png`;
  }

  public handleClose() {
    this.$router.push({ name: 'Home' });
  }
}
</script>
<style lang="scss">
.GalleryImageViewer {
  cursor: pointer;
  position: fixed;
  left: 0;
  top: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.GalleryImageViewerImage {
  max-width: 90vw;
  max-height: 90vh;
}
</style>
