<template>
  <div id="app">
    <h1>Frame Viewer</h1>

    <h2>frames from dir</h2>
    <FrameViewer
      :frames="framesFromDir"
      :thumbnailWidth="160"
      :thumbnailAspectRatio="4 / 3"
      :relativeWidth="true"
    />

    <h2>frames from paths</h2>
    <FrameViewer
      :frames="framesFromPaths"
      :thumbnailWidth="160"
      :thumbnailAspectRatio="4 / 3"
      :relativeWidth="false"
    />
  </div>
</template>

<script>
import FrameViewer from "./components/FrameViewer.vue";

export default {
  name: "App",
  components: {
    FrameViewer
  },
  data: function() {
    return {
      frameDir: "mvn",
      framePrefix: "mvn-",
      frameMaxIndex: 114,
      framesFromPaths: [
        require(`@/assets/mvn/mvn-0.jpg`),
        require(`@/assets/mvn/mvn-1.jpg`),
        require(`@/assets/mvn/mvn-2.jpg`),
        require(`@/assets/mvn/mvn-3.jpg`),
        require(`@/assets/mvn/mvn-4.jpg`),
        require(`@/assets/mvn/mvn-5.jpg`),
        require(`@/assets/mvn/mvn-6.jpg`),
        require(`@/assets/mvn/mvn-7.jpg`),
        require(`@/assets/mvn/mvn-8.jpg`),
        require(`@/assets/mvn/mvn-9.jpg`)
      ]
    };
  },
  computed: {
    framesFromDir() {
      return [...Array(this.frameMaxIndex).keys()].map(i =>
        require(`@/assets/${this.frameDir}/${this.framePrefix}${i}.jpg`)
      );
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
