<template>
  <div id="app">
    <h1>Frame Viewer</h1>
    <!-- <FrameViewer :framePaths="framePathsEpisode"/> -->
    <h2>2005_150509@program</h2>
    <FrameViewer
      :frameDir="frameDir1"
      :framePrefix="framePrefix1"
      :frameMaxIndex="frameMaxIndex1"
    />

    <!-- <h2>2005</h2>
    <FrameViewer :framePaths="framePaths1"/>
    <h2>2011</h2>
    <FrameViewer :framePaths="framePaths2"/>
    <h2>2018</h2>
    <FrameViewer :framePaths="framePaths3"/> -->
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
        "2005_150509@shot/keyframe_13.jpg",
        "2005_150509@shot/keyframe_32.jpg",
        "2005_150509@shot/keyframe_46.jpg",
        "2005_150509@shot/keyframe_50.jpg",
        "2005_150509@shot/keyframe_88.jpg",
        "2005_150509@shot/keyframe_97.jpg",
        "2005_150509@shot/keyframe_122.jpg",
        "2005_150509@shot/keyframe_129.jpg",
        "2005_150509@shot/keyframe_155.jpg",
        "2005_150509@shot/keyframe_163.jpg",
        "2005_150509@shot/keyframe_177.jpg",
        "2005_150509@shot/keyframe_193.jpg",
        "2005_150509@shot/keyframe_215.jpg",
        "2005_150509@shot/keyframe_235.jpg",
        "2005_150509@shot/keyframe_244.jpg",
        "2005_150509@shot/keyframe_263.jpg",
        "2005_150509@shot/keyframe_280.jpg",
        "2005_150509@shot/keyframe_281.jpg",
        "2005_150509@shot/keyframe_324.jpg",
        "2005_150509@shot/keyframe_350.jpg",
        "2005_150509@shot/keyframe_353.jpg",
        "2005_150509@shot/keyframe_375.jpg",
        "2005_150509@shot/keyframe_385.jpg",
        "2005_150509@shot/keyframe_404.jpg",
        "2005_150509@shot/keyframe_414.jpg",
        "2005_150509@shot/keyframe_430.jpg",
        "2005_150509@shot/keyframe_442.jpg",
        "2005_150509@shot/keyframe_460.jpg",
        "2005_150509@shot/keyframe_475.jpg",
        "2005_150509@shot/keyframe_505.jpg",
        "2005_150509@shot/keyframe_525.jpg",
        "2005_150509@shot/keyframe_529.jpg",
        "2005_150509@shot/keyframe_574.jpg",
        "2005_150509@shot/keyframe_588.jpg",
        "2005_150509@shot/keyframe_593.jpg",
        "2005_150509@shot/keyframe_609.jpg",
        "2005_150509@shot/keyframe_624.jpg",
        "2005_150509@shot/keyframe_640.jpg",
        "2005_150509@shot/keyframe_641.jpg",
        "2005_150509@shot/keyframe_663.jpg",
        "2005_150509@shot/keyframe_679.jpg",
        "2005_150509@shot/keyframe_689.jpg",
        "2005_150509@shot/keyframe_705.jpg",
        "2005_150509@shot/keyframe_737.jpg"
      ],
      framePaths2: [
        "2011_3853265@shot/keyframe_4497.jpg",
        "2011_3853265@shot/keyframe_4479.jpg",
        "2011_3853265@shot/keyframe_4482.jpg",
        "2011_3853265@shot/keyframe_4513.jpg",
        "2011_3853265@shot/keyframe_4541.jpg",
        "2011_3853265@shot/keyframe_4564.jpg",
        "2011_3853265@shot/keyframe_4577.jpg",
        "2011_3853265@shot/keyframe_4593.jpg",
        "2011_3853265@shot/keyframe_4610.jpg",
        "2011_3853265@shot/keyframe_4657.jpg",
        "2011_3853265@shot/keyframe_4701.jpg",
        "2011_3853265@shot/keyframe_4743.jpg"
      ],
      framePaths3: [
        "2018_5353716@shot/keyframe_49.jpg",
        "2018_5353716@shot/keyframe_128.jpg",
        "2018_5353716@shot/keyframe_171.jpg"
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
