<template>
  <div class="relative">
    <div
      :style="{
        'background-image': `url(${framesComputed[activeFrame]})`,
        'margin-left': `${thumbnailMargin}px`
      }"
      class="frameviewer-thumbnail"
      ref="frameviewerThumbnail"
    ></div>
    <div ref="frameviewerFrames" @mouseleave="activeFrame = 0">
      <img
        v-for="(frame, index) in framesComputed"
        :key="frame"
        :alt="'frame' + index"
        :src="frame"
        :style="{ width: slitWidthComputed + 'px' }"
        @mouseover="activeFrame = index"
        class="h4 object-fit"
      />
    </div>
    <span>{{ activeFrame }}</span>
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
      slitWidth: 30,
      activeFrame: 0,
      thumbnailWidth: 160,
      thumbnailMargin: 0
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
    framesComputed() {
      return [...Array(this.frameMaxIndex).keys()].map(i =>
        require(`@/assets/${this.frameDir}/${this.framePrefix}${i}.jpg`)
      );
    },
    clientWidth() {
      return document.body.clientWidth || document.documentElement.clientWidth;
    },
    slitWidthRelative() {
      return this.clientWidth / this.frameMaxIndex;
    },
    slitWidthComputed() {
      return this.frameDir ? this.slitWidthRelative : this.slitWidth;
    }
  },
  watch: {
    activeFrame() {
      this.thumbnailMargin = this.calcThumbnailMargin();
    }
  },
  methods: {
    calcThumbnailMargin() {
      let progress = this.activeFrame / this.frameMaxIndex;
      let framesWidth = this.$refs.frameviewerFrames.offsetWidth;
      let x = progress * framesWidth;
      return Math.min(
        Math.max(0, x - this.thumbnailWidth / 2),
        framesWidth - this.thumbnailWidth
      );
    }
  }
};
</script>

<style scoped>
.object-fit {
  object-fit: cover;
}
.frameviewer-thumbnail {
  width: 160px;
  height: 120px;
  background-size: cover;
}
</style>
