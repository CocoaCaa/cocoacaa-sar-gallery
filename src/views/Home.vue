<template>
  <div class="Home">
    <img class="HomeAvatar" src="https://i.imgur.com/bv13JKfm.png" width="200" height="200" />
    <h1 class="HomeTitle">CocoaCaa's Super Animal Royale Gallery</h1>
    <div class="HomeGalleryList">
      <div class="HomeGalleryListItem" v-for="image in images" :key="image.id">
        <GalleryThumbnail
          :imgur-id="image.id"
          :description="image.description"
          @select-image="handleShowGalleryImage"
        />
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script lang="ts">
import ky from 'ky';
import { Options, Vue } from 'vue-class-component';
import GalleryThumbnail from '@/components/GalleryThumbnail.vue';
import { ImgurImage } from '@/types';

@Options({
  components: {
    GalleryThumbnail,
  },
})
export default class Home extends Vue {
  public images: ImgurImage[] = [];

  public async mounted(): Promise<void> {
    const imagesReponse = await ky.get('https://api.imgur.com/3/album/afHytew/images', {
      headers: {
        Authorization: `Client-ID ${process.env.VUE_APP_CLIENT_ID}`,
      },
    });
    const imagesJson: { data: ImgurImage[] } = await imagesReponse.json();
    this.images = imagesJson.data;
  }

  public handleShowGalleryImage(params: { imgurId: string }): void {
    this.$router.push({ name: 'GalleryImage', params: { imgurId: params.imgurId } });
  }
}
</script>
<style lang="scss">
.Home {
  max-width: 1140px;
  margin: 0 auto;
  padding-top: 30px;
}

.HomeAvatar {
  display: block;
  margin: 0 auto;
  border-radius: 100%;
  overflow: hidden;
}

.HomeTitle {
  text-align: center;
  color: #fff;
  padding-top: 15px;
  padding-bottom: 30px;
  margin: 0;
}

.HomeGalleryList {
  display: grid;
  row-gap: 20px;
  grid-template-columns: 1fr;

  @media screen and (min-width: 768px) {
    grid-template-columns: repeat(2, 1fr);
  }

  @media screen and (min-width: 1140px) {
    grid-template-columns: repeat(3, 1fr);
  }
}

.HomeGalleryListItem {
  text-align: center;
}
</style>
