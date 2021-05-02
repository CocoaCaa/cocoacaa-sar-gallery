<template>
  <div>
    <GitHubButton />
    <router-view />
    <footer class="AppFooter">
      <p>Art and website develop by CocoaCaa.</p>
      <p>
        <a href="https://animalroyale.com/" target="_blank">Super Animal Royale</a>
        is copyright
        <a href="https://pixilestudios.com/" target="_blank">Pixile, Inc</a>
        and is not affiliated with this site.
      </p>
    </footer>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import GitHubButton from '@/components/GitHubButton.vue';

@Options({
  components: {
    GitHubButton,
  },
})
export default class App extends Vue {}
</script>

<style lang="scss">
@import '~normalize.css';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #fff;
  background-color: #282a36;
}

.AppFooter {
  padding: 30px 0;
  text-align: center;
}
</style>
