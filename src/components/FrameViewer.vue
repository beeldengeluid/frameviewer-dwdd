<template>
  <div>
    <div>
      <img
        v-for="(framePath, index) in framePathsComputed"
        :key="framePath"
        :alt="'frame' + index"
        :src="require(`@/assets/${framePath}`)"
        :style="{ width: slitWidthComputed + 'px' }"
        class="h4 object-fit"
      />
    </div>
    <div v-if="framePaths">
      <input type="range" min="2" max="170" step="1" v-model="slitWidth" />
      <input type="number" v-model="slitWidth" />
    </div>
  </div>
</template>

<script>
import "../../node_modules/tachyons/css/tachyons.min.css";

export default {
  name: "FrameViewer",
  data: function() {
    return {
      slitWidth: 30
    };
  },
  props: {
    framePaths: { type: Array },
    frameDir: { type: String },
    framePrefix: { type: String },
    frameMaxIndex: { type: Number }
  },
  computed: {
    framePathsComputed() {
      return this.frameDir ? this.framePathsFromDir : this.framePaths;
    },
    framePathsFromDir() {
      return [...Array(this.frameMaxIndex).keys()].map(
        i => `${this.frameDir}/${this.framePrefix}${i}.jpg`
      );
    },
    slitWidthRelative() {
      let clientWidth =
        document.body.clientWidth || document.documentElement.clientWidth;
      return clientWidth / this.frameMaxIndex;
    },
    slitWidthComputed() {
      return this.frameDir ? this.slitWidthRelative : this.slitWidth;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.object-fit {
  object-fit: cover;
}
</style>
