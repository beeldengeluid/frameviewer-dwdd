<template>
  <div>
    <div>
      <img 
        v-for="(framePath, index) in framePaths" :key="framePath"
        :alt="'frame'+index" :src="require(`@/assets/${framePath}`)"
        :style="{ width: slitWidth + 'px' }"
        class="h4 object-fit" 
      >
    </div>
    <input type="range" min="2" max="170" step="1" v-model="slitWidth"> 
    <input type="number" v-model="slitWidth"/>
  </div>
</template>

<script>
import '../../node_modules/tachyons/css/tachyons.min.css';

export default {
  name: 'FrameViewer',
  data: function () {
    return {
      slitWidth: 50
    }
  },
  props: {
    framePaths: {type: Array}
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.object-fit {
  object-fit: cover;
}
</style>
