<template>
<div>
  <my-timer
  :laps="laps"
  :timeDelta="parsedTime"
  @start="startTimer"
  @stop="stopTimer"
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
      hours: 0,
      parsedHours: '',
      minutes: 0,
      parsedMinutes: '',
      seconds: 0,
      milliseconds: 0,
      parsedSeconds: '',
      parsedTime: '',
      timeDelta: 0,
      timeStart: 0,
      timeEnd: 0,
      Timer: 0,
      laps: [
      ]
    }
  },
  methods: {
    
    startTimer(){
      this.isTimerStarted = true;
      this.timeStart = Date.now();
      this.Timer = setInterval(()=>{
        this.timeEnd = Date.now();
        this.timeDelta = this.timeEnd - this.timeStart;
      }, 10);
    },
    stopTimer(){
      this.isTimerStarted = false;
      clearInterval(this.Timer);
    },

    parseTime(){
      this.milliseconds = this.timeDelta%100;
      this.seconds = Math.floor(this.timeDelta/1000)%60;
      this.minutes = Math.floor(this.timeDelta/1000/60)%60;
      this.hours = Math.floor(this.timeDelta/1000/60/60)%60;
      this.parsedMSeconds = this.parseTimeUnit(this.milliseconds);
      this.parsedSeconds = this.parseTimeUnit(this.seconds);
      this.parsedMinutes = this.parseTimeUnit(this.minutes);
      this.parsedHours = this.parseTimeUnit(this.hours);
      this.parsedTime = `${this.parsedHours}:${this.parsedMinutes}:${this.parsedSeconds}:${this.parsedMSeconds}`;
    },
    parseTimeUnit(timeUnit){
      if (timeUnit<10){
        return `0${timeUnit}`
      }
      return `${timeUnit}`
    },
    createLap(){
      if(this.isTimerStarted){
        let lap = {id: this.laps.length+1, h:this.hours, m:this.minutes, s:this.seconds, ms:this.milliseconds};
        this.laps.push(lap);
      }
    }
  },

  mounted() {
    this.parseTime();
  },

  watch:{
    timeDelta(){
      this.parseTime();
    }
  }
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
