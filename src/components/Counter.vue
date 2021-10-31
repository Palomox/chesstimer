<template>
  <div>
    <span :style="'background-color: '+color" class="color"></span>
    <h1 :textContent="formattedTime"></h1>
    <button @click="pass()" :disabled="disabled">Pass</button>
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';

@Options({
  name: 'counter',
  props: {
    time: Number,
    color: String,
    disabled: Boolean
  },
  computed:{
    //formattedTime: function (){},
  }
})
export default class Counter extends Vue {
  time !: number

  get formattedTime(){
    if(this.time%60 < 10){
      return Math.trunc(this.time/60)+":0"+this.time%60;
    }
    return Math.trunc(this.time/60)+":"+(this.time%60);

  }

  pass(){
    this.$emit('pass')
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@tailwind base;
@tailwind components;
@tailwind utilities;

div{
  @apply text-white flex flex-col items-center;
}
div > h1{
  @apply text-9xl;
}
button{
  @apply text-2xl border border-black rounded pl-1 pr-1 pt-0.5 pb-0.5 bg-gray-700;
}

.color{
  @apply w-32 h-32 block rounded-xl;
}
</style>
