<template>
  <div id="app">
    <h1>Frame Viewer</h1>

    <h2>Single frameLine image</h2>
    <FrameViewer
      :frameLine="frameLine"
      :frames="frames"
      :dates="dates"
      :thumbnailWidth="160"
      :thumbnailAspectRatio="4 / 3"
    />

    <h2>Individual frames - responsive full width</h2>
    <FrameViewer
      :frames="frames"
      :dates="dates"
      :thumbnailWidth="160"
      :thumbnailAspectRatio="4 / 3"
    />

    <h2>Individual frames - custom fixed width</h2>
    <FrameViewer
      :frames="frames"
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
      slitWidthCustom: 10,
      frameLine: require(`@/assets/mvn/frameline.jpg`),
      frameDir: "mvn",
      frameFileNames: [
        "2005-10-11_151531@program.jpg",
        "2005-11-09_127931@program.jpg",
        "2005-12-09_150478@program.jpg",
        "2006-01-13_185378@program.jpg",
        "2006-02-16_185450@program.jpg",
        "2006-03-14_30706@program.jpg",
        "2006-04-11_34447@program.jpg",
        "2006-09-06_61896@program.jpg",
        "2006-10-10_68533@program.jpg",
        "2006-11-09_76846@program.jpg",
        "2006-12-22_92584@program.jpg",
        "2007-01-10_94667@program.jpg",
        "2007-02-06_99691@program.jpg",
        "2007-03-21_394638@program.jpg",
        "2007-04-13_401177@program.jpg",
        "2007-09-06_760300@program.jpg",
        "2007-10-09_811800@program.jpg",
        "2007-11-07_852162@program.jpg",
        "2007-12-06_877529@program.jpg",
        "2008-01-04_896126@program.jpg",
        "2008-02-12_921287@program.jpg",
        "2008-03-06_941108@program.jpg",
        "2008-04-02_958884@program.jpg",
        "2008-05-05_970062@program.jpg",
        "2008-09-03_996152@program.jpg",
        "2008-10-06_1004132@program.jpg",
        "2008-11-10_1010959@program.jpg",
        "2008-12-15_1019716@program.jpg",
        "2009-01-19_1026970@program.jpg",
        "2009-02-13_1044281@program.jpg",
        "2009-03-27_1053818@program.jpg",
        "2009-04-20_1115877@program.jpg",
        "2009-05-11_2034698@program.jpg",
        "2009-09-01_3277342@program.jpg",
        "2009-10-07_3286729@program.jpg",
        "2009-11-10_3293613@program.jpg",
        "2009-12-16_3302109@program.jpg",
        "2010-01-19_3327704@program.jpg",
        "2010-02-04_3332570@program.jpg",
        "2010-03-05_3611967@program.jpg",
        "2010-04-13_3743130@program.jpg",
        "2010-05-12_3759243@program.jpg",
        "2010-06-03_3766981@program.jpg",
        "2010-09-08_3820740@program.jpg",
        "2010-10-04_3826796@program.jpg",
        "2010-11-04_3834657@program.jpg",
        "2010-12-01_3839894@program.jpg",
        "2011-01-28_3851050@program.jpg",
        "2011-02-10_3853970@program.jpg",
        "2011-03-17_3863864@program.jpg",
        "2011-04-06_3874716@program.jpg",
        "2011-05-03_3887376@program.jpg",
        "2011-09-08_3917507@program.jpg",
        "2011-10-13_3927186@program.jpg",
        "2011-11-15_3934679@program.jpg",
        "2011-12-05_3939936@program.jpg",
        "2012-01-12_3948664@program.jpg",
        "2012-02-10_3955103@program.jpg",
        "2012-03-22_3965077@program.jpg",
        "2012-04-19_3972205@program.jpg",
        "2012-05-02_3974862@program.jpg",
        "2012-09-11_4003292@program.jpg",
        "2012-10-12_4018775@program.jpg",
        "2012-11-09_4026402@program.jpg",
        "2012-12-05_4032376@program.jpg",
        "2013-01-14_4048408@program.jpg",
        "2013-02-25_4058636@program.jpg",
        "2013-03-21_4083522@program.jpg",
        "2013-04-23_4090834@program.jpg",
        "2013-05-24_4146098@program.jpg",
        "2013-09-09_4169736@program.jpg",
        "2013-10-07_4189960@program.jpg",
        "2013-11-06_4197244@program.jpg",
        "2013-12-03_4202328@program.jpg",
        "2014-01-08_4208679@program.jpg",
        "2014-02-26_4230034@program.jpg",
        "2014-03-17_4235727@program.jpg",
        "2014-04-11_4241847@program.jpg",
        "2014-05-14_4258324@program.jpg",
        "2014-09-09_4285734@program.jpg",
        "2014-10-13_4296542@program.jpg",
        "2014-11-14_4313544@program.jpg",
        "2014-12-02_4330488@program.jpg",
        "2015-01-14_4427713@program.jpg",
        "2015-02-10_4454554@program.jpg",
        "2015-03-13_4462732@program.jpg",
        "2015-04-21_4475492@program.jpg",
        "2015-05-07_4483316@program.jpg",
        "2015-08-31_4507541@program.jpg",
        "2015-09-11_4510086@program.jpg",
        "2015-10-15_4528862@program.jpg",
        "2015-11-20_4537666@program.jpg",
        "2015-12-10_4618240@program.jpg",
        "2016-01-18_4885399@program.jpg",
        "2016-02-11_4948800@program.jpg",
        "2016-03-21_5002008@program.jpg",
        "2016-04-18_5123416@program.jpg",
        "2016-05-19_5231766@program.jpg",
        "2016-08-25_5249986@program.jpg",
        "2016-09-16_5254635@program.jpg",
        "2016-10-03_5258307@program.jpg",
        "2016-11-09_5265597@program.jpg",
        "2016-12-05_5270610@program.jpg",
        "2017-01-17_5278684@program.jpg",
        "2017-02-02_5281699@program.jpg",
        "2017-03-16_5290249@program.jpg",
        "2017-04-13_5295863@program.jpg",
        "2017-05-03_5299540@program.jpg",
        "2017-09-27_5329010@program.jpg",
        "2017-10-11_5331747@program.jpg",
        "2017-11-16_5339363@program.jpg",
        "2017-12-11_5344676@program.jpg",
        "2018-01-25_5353532@program.jpg",
        "2018-02-13_5357425@program.jpg",
        "2018-03-20_5364597@program.jpg"
      ]
    };
  },
  computed: {
    frames() {
      return this.frameFileNames.map(fn =>
        require(`@/assets/${this.frameDir}/${fn}`)
      );
    },
    dates() {
      return this.frameFileNames.map(fn => fn.split("_")[0]);
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
