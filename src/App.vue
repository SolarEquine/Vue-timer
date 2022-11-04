<template>
<div>
  <my-timer
  :laps="laps"
  :time="timeDelta"
  :isTimerStarted="isTimerStarted"
  @toggle="toggleTimer"
  @lap="createLap"
  ></my-timer>
</div>
</template>

<script>
import MyTimer from "@/components/MyTimer";

export default {

  components: {
    MyTimer,
  },

  data(){
    return{
      isTimerStarted: false,
      timeDelta: 0,
      lapDelta: 0,
      timeStart: 0,
      timeEnd: 0,
      Timer: 0,
      laps: [
      ]
    }
  },
  methods: {
    
    startTimer(){
      if(!this.isTimerStarted){
        this.isTimerStarted = true;
        this.laps= []
        this.timeStart = Date.now();
        this.Timer = setInterval(()=>{
          this.timeEnd = Date.now();
          this.timeDelta = this.timeEnd - this.timeStart;
      }, 10);
      }
    },
    stopTimer(){
      this.isTimerStarted = false;
      clearInterval(this.Timer);
    },
    toggleTimer(){
      if(this.isTimerStarted){
        this.createLap();
        this.stopTimer();
      }
      else{
        this.startTimer();
      }
    },
    createLap(){
      if(this.isTimerStarted){
        if(this.laps.length>0){
          this.lapDelta = this.timeDelta - this.laps[this.laps.length-1].lapTime
        }
        else{
          this.lapDelta = this.timeDelta;
        }
        let lap = {id: this.laps.length+1, lapTime:this.timeDelta, delta:this.lapDelta};
        console.log(lap)
        this.laps.push(lap);
      }
    }
  },

}
</script>

<style>
*{
  margin: 0;
  padding: 0;
}

@import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

body{
  background: linear-gradient(#BA324F 0%,  #175676 100%);

}


</style>
