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
          :style="{ width: slitWidth }"
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
  </div>
</template>

<script>
export default {
  name: "FrameViewer",
  data: function() {
    return {
      activeFrame: undefined,
      thumbnailMargin: undefined,
      thumbnailSrc: undefined
    };
  },
  props: {
    frameLine: { type: String, required: false },
    frames: { type: Array, required: true },
    thumbnailWidth: { type: Number, required: true },
    thumbnailAspectRatio: { type: Number, default: 4 / 3 },
    slitWidthCustom: { type: undefined, required: false }
  },
  computed: {
    clientWidth() {
      return document.body.clientWidth || document.documentElement.clientWidth;
    },
    slitWidthRelative() {
      return 100 / this.frames.length;
    },
    slitWidth() {
      return this.slitWidthCustom
        ? this.slitWidthCustom + "px"
        : this.slitWidthRelative + "%";
    },
    thumbnailHeight() {
      return this.thumbnailWidth / this.thumbnailAspectRatio;
    }
  },
  watch: {
    activeFrame() {
      // set Thumbnail
      this.thumbnailSrc = this.frames[this.activeFrame];
      // move Thumbnail
      let progress = this.activeFrame / this.frames.length;
      let x = progress * this.$refs.frameviewerFrames.offsetWidth;
      this.moveThumbnail(x);
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
