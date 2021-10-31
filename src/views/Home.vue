<template>
  <div class="popupContainer">
    <div>
      <popup class="popup" bgColor="#1E40AF" msg="There are some keybindings:<br/>
  Press 's' to start <br/>
  Press 'p' to pass the turn<br/>
  Press 'shift + p' to pause"/>
    </div>
  </div>

  <span class="line"/>
  <div class="all">
    <div class="main-container">
      <counter color="white" :disabled="this.current != 1" @pass="switchPlayer()" :time="timeFirst"/>
      <counter color="black" :disabled="this.current != 2" @pass="switchPlayer()" :time="timeSecond"/>
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
import Popup from "@/components/Popup.vue";


@Options({
  components: {
    Popup,
    Counter,
  },
})
export default class Home extends Vue {
  timeFirst: number = 600
  timeSecond: number = 600
  current: number = 1
  paused: boolean = false

  mounted() {
    window.addEventListener("keypress", ev => {
      switch (ev.key) {
        case 's':
          this.start();
          break;
        case 'p':
          this.switchPlayer();
          break;
        case 'P':
          this.pause();
          break;
      }
    })
  }

  start() {
    window.setInterval(this.decrease, 1000)
  }

  pause() {
    this.paused = !this.paused;
  }

  switchPlayer() {
    if (this.current == 1) {
      this.current = 2;
    } else {
      this.current = 1;
    }

  }


  decrease() {
    if (this.paused) {
      return;
    }
    switch (this.current) {
      case 1:
        if (this.timeFirst == 0) {
          return;
        }
        this.timeFirst--;
        break;
      case 2:
        if (this.timeSecond == 0) {
          return;
        }
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

.controls {
  @apply flex flex-row gap-4;
}

.line {
  @apply absolute bg-black;
  margin-left: 49.8vw;
  width: 0.4vw;
  height: 45%;
}


.popupContainer {
  @apply relative mt-6;
}
.popupContainer > div{
  @apply flex flex-row justify-center items-center
}
</style>
