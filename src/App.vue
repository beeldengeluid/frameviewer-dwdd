<template>
  <div id="app">
    <h1>Frame Viewer</h1>

    <h2>Single frameLine image</h2>
    <FrameViewer
      :frameLine="frameLine"
      :frames="framesFromDir"
      :dates="dates"
      :thumbnailWidth="160"
      :thumbnailAspectRatio="4 / 3"
    />

    <h2>Individual frames - responsive full width</h2>
    <FrameViewer
      :frames="framesFromDir"
      :dates="dates"
      :thumbnailWidth="160"
      :thumbnailAspectRatio="4 / 3"
    />

    <h2>Individual frames - custom fixed width</h2>
    <FrameViewer
      :frames="framesFromPaths"
      :dates="dates"
      :thumbnailWidth="160"
      :thumbnailAspectRatio="4 / 3"
      :slitWidthCustom="slitWidthCustom"
    />
    <div>
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
      frameLine: require(`@/assets/mvn/frameline.jpg`),
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
      ],
      dates: [
        "2005-10-11",
        "2005-11-09",
        "2005-12-09",
        "2006-01-13",
        "2006-02-16",
        "2006-03-14",
        "2006-04-11",
        "2006-09-06",
        "2006-10-10",
        "2006-11-09",
        "2006-12-22",
        "2007-01-10",
        "2007-02-06",
        "2007-03-21",
        "2007-04-13",
        "2007-09-06",
        "2007-10-09",
        "2007-11-07",
        "2007-12-06",
        "2008-01-04",
        "2008-02-12",
        "2008-03-06",
        "2008-04-02",
        "2008-05-05",
        "2008-09-03",
        "2008-10-06",
        "2008-11-10",
        "2008-12-15",
        "2009-01-19",
        "2009-02-13",
        "2009-03-27",
        "2009-04-20",
        "2009-05-11",
        "2009-09-01",
        "2009-10-07",
        "2009-11-10",
        "2009-12-16",
        "2010-01-19",
        "2010-02-04",
        "2010-03-05",
        "2010-04-13",
        "2010-05-12",
        "2010-06-03",
        "2010-09-08",
        "2010-10-04",
        "2010-11-04",
        "2010-12-01",
        "2011-01-28",
        "2011-02-10",
        "2011-03-17",
        "2011-04-06",
        "2011-05-03",
        "2011-09-08",
        "2011-10-13",
        "2011-11-15",
        "2011-12-05",
        "2012-01-12",
        "2012-02-10",
        "2012-03-22",
        "2012-04-19",
        "2012-05-02",
        "2012-09-11",
        "2012-10-12",
        "2012-11-09",
        "2012-12-05",
        "2013-01-14",
        "2013-02-25",
        "2013-03-21",
        "2013-04-23",
        "2013-05-24",
        "2013-09-09",
        "2013-10-07",
        "2013-11-06",
        "2013-12-03",
        "2014-01-08",
        "2014-02-26",
        "2014-03-17",
        "2014-04-11",
        "2014-05-14",
        "2014-09-09",
        "2014-10-13",
        "2014-11-14",
        "2014-12-02",
        "2015-01-14",
        "2015-02-10",
        "2015-03-13",
        "2015-04-21",
        "2015-05-07",
        "2015-08-31",
        "2015-09-11",
        "2015-10-15",
        "2015-11-20",
        "2015-12-10",
        "2016-01-18",
        "2016-02-11",
        "2016-03-21",
        "2016-04-18",
        "2016-05-19",
        "2016-08-25",
        "2016-09-16",
        "2016-10-03",
        "2016-11-09",
        "2016-12-05",
        "2017-01-17",
        "2017-02-02",
        "2017-03-16",
        "2017-04-13",
        "2017-05-03",
        "2017-09-27",
        "2017-10-11",
        "2017-11-16",
        "2017-12-11",
        "2018-01-25",
        "2018-02-13",
        "2018-03-20"
      ],
      slitWidthCustom: 50
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
