<template>
  <span class="line"/>
  <div class="all">
    <div class="main-container">
      <counter color="white" :disabled="this.current != 1" @pass="switchPlayer(2)" :time="timeFirst"/>
      <counter color="black" :disabled="this.current != 2" @pass="switchPlayer(1)" :time="timeSecond"/>
    </div>
    <div class="controls">
      <button @click="this.start()">Start</button>
      <button @click="this.pause()">Pause</button>
    </div>
  </div>
</template>

<script lang="ts">
import {Options, Vue} from 'vue-class-component';
import Counter from "@/components/Counter.vue";


@Options({
  components: {
    Counter,
  },
})
export default class Home extends Vue {
  timeFirst: number = 600
  timeSecond: number = 600
  current: number = 1
  paused: boolean = false
  start() {
    window.setInterval(this.decrease, 1000)
  }

  pause(){
    this.paused = !this.paused;
  }
  switchPlayer(to: number) {
    this.current = to;
  }


  decrease() {
    if(this.paused){
      return;
    }
    switch (this.current) {
      case 1:
        this.timeFirst--;
        break;
      case 2:
        this.timeSecond--;
        break;
    }
  }
}
</script>
<style>
@tailwind base;
@tailwind components;
@tailwind utilities;

.all {
  @apply flex flex-col gap-4 items-center mt-6 text-white text-2xl;
}

.main-container {
  @apply flex flex-row gap-20;
}

button {
  @apply border border-black rounded pl-1 pr-1 pt-0.5 pb-0.5 bg-gray-700;
}
.controls{
  @apply flex flex-row gap-4;
}
.line{
  @apply absolute bg-black;
  margin-left: 50%;
  width: 2px;
  height: 45%;
}
</style>
