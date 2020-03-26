<template>
  <div class="frameviewer">
    <div class="frameviewer-frames" ref="frameviewerFrames">
      <div v-if="frameLine">
        <img
          :src="frameLine"
          @mousemove="onFrameLineMouseMove"
          alt="frameline"
        />
      </div>
      <div v-else>
        <img
          class="frameviewer-frame"
          v-for="(frame, index) in frames"
          :key="frame"
          :alt="'frame' + index"
          :src="frame"
          :style="{ width: slitWidth + 'px' }"
          @mouseover="activeFrame = index"
        />
      </div>
    </div>
    <div
      class="frameviewer-thumbnail"
      :style="{
        'background-image': `url(${thumbnailSrc})`,
        'margin-left': `${thumbnailMargin}px`,
        width: `${thumbnailWidth}px`,
        height: `${thumbnailHeight}px`
      }"
    ></div>
    <div v-if="!relativeWidth">
      <div>{{ activeFrame }}</div>
      <input
        type="range"
        min="2"
        max="170"
        step="1"
        v-model="slitWidthCustom"
      />
      <input type="number" v-model="slitWidthCustom" />
    </div>
  </div>
</template>

<script>
export default {
  name: "FrameViewer",
  data: function() {
    return {
      slitWidthCustom: 50,
      activeFrame: undefined,
      thumbnailMargin: undefined,
      thumbnailSrc: undefined
    };
  },
  props: {
    frameLine: { type: String },
    frames: { type: Array },
    thumbnailWidth: { type: Number },
    thumbnailAspectRatio: { type: Number },
    relativeWidth: { type: Boolean }
  },
  computed: {
    clientWidth() {
      return document.body.clientWidth || document.documentElement.clientWidth;
    },
    slitWidthRelative() {
      return this.clientWidth / this.frames.length;
    },
    slitWidth() {
      return this.relativeWidth ? this.slitWidthRelative : this.slitWidthCustom;
    },
    thumbnailHeight() {
      return this.thumbnailWidth / this.thumbnailAspectRatio;
    }
  },
  watch: {
    activeFrame() {
      let progress = this.activeFrame / this.frames.length;
      let x = progress * this.$refs.frameviewerFrames.offsetWidth;
      this.moveThumbnail(x);
      this.thumbnailSrc = this.frames[this.activeFrame];
    }
  },
  methods: {
    onFrameLineMouseMove(event) {
      this.setThumbnail(event.offsetX);
      this.moveThumbnail(event.offsetX);
    },
    setThumbnail(offsetX) {
      let framesWidth = this.$refs.frameviewerFrames.offsetWidth;
      let frameIndex = Math.round((offsetX / framesWidth) * this.frames.length);
      this.thumbnailSrc = this.frames[frameIndex];
    },
    moveThumbnail(offsetX) {
      let framesWidth = this.$refs.frameviewerFrames.offsetWidth;
      this.thumbnailMargin = Math.min(
        Math.max(0, offsetX - this.thumbnailWidth / 2),
        framesWidth - this.thumbnailWidth
      );
    }
  }
};
</script>

<style scoped>
.frameviewer {
  position: relative;
  display: inline-block;
}
.frameviewer .frameviewer-thumbnail {
  position: absolute;
  top: 0;
  transform: translateY(-100%) translateY(-7px);
  transition: opacity 0.2s, z-index 0.2s;
  background-size: cover;
  background-position: center;
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
