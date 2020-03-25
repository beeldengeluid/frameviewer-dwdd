<template>
  <div class="frameviewer">
    <div
      class="frameviewer-frames"
      ref="frameviewerFrames"
    >
      <img
        class="frameviewer-frame"
        v-for="(frame, index) in framesComputed"
        :key="frame"
        :alt="'frame' + index"
        :src="frame"
        :style="{ width: slitWidthComputed + 'px' }"
        @mouseover="activeFrame = index"
      />
    </div>
    <div
      class="frameviewer-thumbnail"
      :style="{
        'background-image': `url(${framesComputed[activeFrame]})`,
        'margin-left': `${thumbnailMargin}px`,
        'width': `${thumbnailWidth}px`,
        'height': `${thumbnailHeight}px`
      }"
    ></div>
    <span>{{ activeFrame }}</span>
    <div v-if="framePaths">
      <input type="range" min="2" max="170" step="1" v-model="slitWidth" />
      <input type="number" v-model="slitWidth" />
    </div>
  </div>
</template>

<script>
export default {
  name: "FrameViewer",
  data: function() {
    return {
      slitWidth: 30,
      activeFrame: 0,
      thumbnailMargin: 0
    };
  },
  props: {
    framePaths: { type: Array },
    frameDir: { type: String },
    framePrefix: { type: String },
    frameMaxIndex: { type: Number },
    thumbnailWidth: { type: Number },
    thumbnailAspectRatio: { type: Number }
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
    },
    thumbnailHeight() {
      return this.thumbnailWidth / this.thumbnailAspectRatio;
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
.frameviewer {
  position: relative;
}
.frameviewer .frameviewer-thumbnail {
  position: absolute;
  top: 0;
  transform: translateY(-100%) translateY(-7px);
  transition: opacity 0.2s, z-index 0.2s;
  /*width: 160px;*/
  height: 120px;
  background-size: cover;
  border: solid rgba(28, 28, 28, 0.9) 3px;
  border-radius: 3px;
  z-index: -1;
  opacity: 0;
}
.frameviewer .frameviewer-frame {
  height: 100px;
  object-fit: cover;
}
.frameviewer .frameviewer-frames:hover + .frameviewer-thumbnail {
  z-index: 999;
  opacity: 1;
}
</style>
