<template>
  <button
    class="GalleryThumbnail"
    :style="{ 'background-image': `url(${src})` }"
    @click="$emit('select-image', { imgurId })"
  >
    <div class="GalleryThumbnailDescription">{{ description }}</div>
  </button>
</template>
<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options<GalleryThumbnail>({
  props: {
    imgurId: String,
    description: String,
  },
  watch: {
    imgurId: {
      handler(imgurId: string) {
        this.fetchImage(imgurId);
      },
      immediate: true,
    },
  },
})
export default class GalleryThumbnail extends Vue {
  private src: string | null = null;

  public fetchImage(imgurId: string) {
    this.src = `https://i.imgur.com/${imgurId}s.png`;
    const img = new Image();
    img.onload = () => {
      this.src = img.src;
    };
    img.src = `https://i.imgur.com/${imgurId}.png`;
  }
}
</script>
<style lang="scss">
.GalleryThumbnail {
  cursor: pointer;
  position: relative;
  display: inline-block;
  width: 350px;
  height: 350px;
  background-size: cover;
  background-position: center;
  box-shadow: 10px 10px 0 rgba(255, 255, 255, 0.2);
  transition: 200ms box-shadow, 200ms transform;
  overflow: hidden;
  border: 0;
  background-color: none;

  &:hover {
    box-shadow: 0 0 0 rgba(255, 255, 255, 0.2);
    transform: translate(10px, 10px);

    .GalleryThumbnailDescription {
      transform: translateY(0);
    }
  }
}

.GalleryThumbnailDescription {
  position: absolute;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
  padding: 15px 0;
  color: #fff;
  font-weight: bold;
  transform: translateY(100%);
  transition: 200ms transform;
}
</style>
