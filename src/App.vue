<template>
<div class="container">
  <stopwatch-block></stopwatch-block>
</div>
</template>
<script>
import StopwatchBlock from "./components/StopwatchBlock.vue";
export default {
  components:{
    StopwatchBlock
  }
}
</script>

<style scoped>
.container{
  display: flex;
  justify-content: center;
  padding: 30px;

  font-family: "Gotham Pro",serif;
}
</style>
