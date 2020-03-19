<template>
  <div id="app">
    <h1>Frame Viewer</h1>

    <h2>2005</h2>
    <FrameViewer :framePaths="framePaths1"/>
    <h2>2011</h2>
    <FrameViewer :framePaths="framePaths2"/>
    <h2>2018</h2>
    <FrameViewer :framePaths="framePaths3"/>
  </div>
</template>

<script>
import FrameViewer from './components/FrameViewer.vue'

export default {
  name: 'App',
  data: function () {
    return {
      framePaths1: [
        '2005_150509@program/keyframe_13.jpg',
        '2005_150509@program/keyframe_32.jpg',
        '2005_150509@program/keyframe_46.jpg',
        '2005_150509@program/keyframe_50.jpg',
        '2005_150509@program/keyframe_88.jpg',
        '2005_150509@program/keyframe_97.jpg',
        '2005_150509@program/keyframe_122.jpg',
        '2005_150509@program/keyframe_129.jpg',
        '2005_150509@program/keyframe_155.jpg',
        '2005_150509@program/keyframe_163.jpg',
        '2005_150509@program/keyframe_177.jpg',
        '2005_150509@program/keyframe_193.jpg',
        '2005_150509@program/keyframe_215.jpg',
        '2005_150509@program/keyframe_235.jpg',
        '2005_150509@program/keyframe_244.jpg',
        '2005_150509@program/keyframe_263.jpg',
        '2005_150509@program/keyframe_280.jpg',
        '2005_150509@program/keyframe_281.jpg',
        '2005_150509@program/keyframe_324.jpg',
        '2005_150509@program/keyframe_350.jpg',
        '2005_150509@program/keyframe_353.jpg',
        '2005_150509@program/keyframe_375.jpg',
        '2005_150509@program/keyframe_385.jpg',
        '2005_150509@program/keyframe_404.jpg',
        '2005_150509@program/keyframe_414.jpg',
        '2005_150509@program/keyframe_430.jpg',
        '2005_150509@program/keyframe_442.jpg',
        '2005_150509@program/keyframe_460.jpg',
        '2005_150509@program/keyframe_475.jpg',
        '2005_150509@program/keyframe_505.jpg',
        '2005_150509@program/keyframe_525.jpg',
        '2005_150509@program/keyframe_529.jpg',
        '2005_150509@program/keyframe_574.jpg',
        '2005_150509@program/keyframe_588.jpg',
        '2005_150509@program/keyframe_593.jpg',
        '2005_150509@program/keyframe_609.jpg',
        '2005_150509@program/keyframe_624.jpg',
        '2005_150509@program/keyframe_640.jpg',
        '2005_150509@program/keyframe_641.jpg',
        '2005_150509@program/keyframe_663.jpg',
        '2005_150509@program/keyframe_679.jpg',
        '2005_150509@program/keyframe_689.jpg',
        '2005_150509@program/keyframe_705.jpg',
        '2005_150509@program/keyframe_737.jpg',
      ],
      framePaths2: [
        '2011_3853265@program/keyframe_4497.jpg',
        '2011_3853265@program/keyframe_4479.jpg',
        '2011_3853265@program/keyframe_4482.jpg',
        '2011_3853265@program/keyframe_4513.jpg',
        '2011_3853265@program/keyframe_4541.jpg',
        '2011_3853265@program/keyframe_4564.jpg',
        '2011_3853265@program/keyframe_4577.jpg',
        '2011_3853265@program/keyframe_4593.jpg',
        '2011_3853265@program/keyframe_4610.jpg',
        '2011_3853265@program/keyframe_4657.jpg',
        '2011_3853265@program/keyframe_4701.jpg',
        '2011_3853265@program/keyframe_4743.jpg',
      ],
      framePaths3: [
        '2018_5353716@program/keyframe_49.jpg',
        '2018_5353716@program/keyframe_128.jpg',
        '2018_5353716@program/keyframe_171.jpg',
      ],

    }
  },
  components: {
    FrameViewer
  }
}
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
