<template>
  <div class="frameviewer">
    <div class="frameviewer-frames" ref="frameviewerFrames">
      <div v-if="frameLine">
        <img
          class="frameviewer-frameline"
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
    >
      <div class="frameviewer-date">{{ thumbnailDate }}</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "FrameViewer",
  data: function() {
    return {
      activeFrame: undefined,
      thumbnailMargin: undefined,
      thumbnailSrc: undefined,
      thumbnailDate: undefined
    };
  },
  props: {
    frameLine: { type: String, required: false },
    frames: { type: Array, required: true },
    labels: { type: Array, required: false },
    thumbnailWidth: { type: Number, required: true },
    thumbnailAspectRatio: { type: Number, default: 4 / 3 },
    slitWidthCustom: { type: undefined, required: false }
  },
  computed: {
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
      // this.thumbnailSrc = this.frames[this.activeFrame];
      this.setThumbnailSrc(this.activeFrame);
      this.setThumbnailDate(this.activeFrame);
      // move Thumbnail
      let progress = this.activeFrame / this.frames.length;
      let x = progress * this.$refs.frameviewerFrames.offsetWidth;
      this.moveThumbnail(x);
    }
  },
  methods: {
    getActiveIndex(offsetX) {
      let framesWidth = this.$refs.frameviewerFrames.offsetWidth;
      return Math.round((offsetX / framesWidth) * (this.frames.length - 1));
    },
    onFrameLineMouseMove(event) {
      let activeIndex = this.getActiveIndex(event.offsetX);
      this.setThumbnailSrc(activeIndex);
      this.setThumbnailDate(activeIndex);
      this.moveThumbnail(event.offsetX);
    },
    setThumbnailSrc(activeIndex) {
      this.thumbnailSrc = this.frames[activeIndex];
    },
    setThumbnailDate(activeIndex) {
      if (this.labels) {
        this.thumbnailDate = this.labels[activeIndex];
      }
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
  display: flex;
  justify-content: center;
}
.frameviewer .frameviewer-thumbnail .frameviewer-date {
  color: #eee;
  background: rgba(28, 28, 28, 0.9);
  font-size: 0.9rem;
  padding-left: 0.25rem;
  padding-right: 0.25rem;
  position: absolute;
  bottom: 0;
}
.frameviewer .frameviewer-frame {
  height: 100px;
  object-fit: cover;
}
.frameviewer img.frameviewer-frameline {
  width: 100%;
}
.frameviewer .frameviewer-frames:hover + .frameviewer-thumbnail {
  z-index: 999;
  opacity: 1;
}
</style>
