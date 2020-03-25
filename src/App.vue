<template>
  <div id="app">
    <h1>Frame Viewer</h1>
    <!-- <FrameViewer :framePaths="framePathsEpisode"/> -->
    <h2>via frameDir prop</h2>
    <FrameViewer
      :frameDir="frameDir1"
      :framePrefix="framePrefix1"
      :frameMaxIndex="frameMaxIndex1"
    />

    <h2>via framePaths prop</h2>
    <FrameViewer :framePaths="framePaths1"/>
  </div>
</template>

<script>
import FrameViewer from "./components/FrameViewer.vue";

export default {
  name: "App",
  data: function() {
    return {
      frameDir1: "mvn",
      framePrefix1: "mvn-",
      frameMaxIndex1: 114,
      framePaths1: [
        "mvn/mvn-0.jpg",
        "mvn/mvn-1.jpg",
        "mvn/mvn-2.jpg",
        "mvn/mvn-3.jpg",
        "mvn/mvn-4.jpg",
        "mvn/mvn-5.jpg",
        "mvn/mvn-6.jpg",
        "mvn/mvn-7.jpg",
        "mvn/mvn-8.jpg",
        "mvn/mvn-9.jpg"
      ]
    };
  },
  components: {
    FrameViewer
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
