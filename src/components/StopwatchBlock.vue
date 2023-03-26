<template>
  <div class="container_block">
    <StopwatchItem v-for="item in listStopwatch" :key="item.id"/>
    <div class="container_stopwatch_add" @click="addStopwatch">
      <div class="stopwatch_symbol_plus">
      </div>
    </div>
  </div>
</template>

<script>
import StopwatchItem from "./StopwatchItem.vue";

export default {
  name: "StopwatchBlock",
  components: {StopwatchItem},
  data() {
    return {
      listStopwatch: [{id: new Date()}, {id: new Date()}]
    }
  },
  methods: {
    addStopwatch() {
      this.listStopwatch = [...this.listStopwatch, {id: new Date()}]
    }
  }

}
</script>

<style scoped>

.container_block {

  max-width: max-content;
  max-height: max-content;

  display: grid;
  gap: 45px 50px;
}

.container_stopwatch_add {
  width: 225px;
  height: 120px;
  display: flex;
  align-items: center;
  justify-content: center;

  background: #696969;

  font-size: 20px;
  font-weight: bold;
  color: #9E9E9E;

  cursor: pointer;
}

.stopwatch_symbol_plus {
  width: 20px;
  height: 20px;
  position: relative;
}

.stopwatch_symbol_plus::after {
  content: " ";
  position: absolute;
  display: block;
  background-color: #9E9E9E;
  height: 2px;
  top: 9px;
  right: 0;
  left: 0;
  z-index: 9;
}

.stopwatch_symbol_plus::before {
  content: " ";
  position: absolute;
  display: block;
  background-color: #9E9E9E;
  width: 2px;
  left: 9px;
  top: 0;
  bottom: 0;
  z-index: 9;
}

@media (min-width: 320px) {
  .container_block {
    grid-template-columns: repeat(1, auto);
  }
}


@media (min-width: 768px) {
  .container_block {
    grid-template-columns: repeat(2, auto);
  }
}


@media (min-width: 1024px) {
  .container_block {
    grid-template-columns: repeat(3, auto);
  }
}

</style>