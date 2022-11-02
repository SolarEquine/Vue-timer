<template>
<div>
  <div class="timer">
    <div class="container">
      <div class="timer__inner">
        <div
          class="timer__body"
          >
          {{ parsedTime }}
        </div>
        <div class="timer__controls">
          <button @click="startTimer">Старт</button>
          <button @click="stopTimer">Стоп</button>
          <button @click="createLap">Круг</button>
        </div>
        <div class="timer__laps">
          <div class="laps">
            <div
              v-for="lap in laps.slice().reverse()"
              :key="lap.id"
             class="lap">{{lap.id}}: {{lap.h}}:{{lap.m}}:{{lap.s}}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>


export default {

  data(){
    return{
      isTimerStarted: false,
      hours: 0,
      parsedHours: '',
      minutes: 0,
      parsedMinutes: '',
      seconds: 0,
      parsedSeconds: '',
      parsedTime: '',
      fullTime: 0,
      Timer: 0,
      laps: [
      ]
    }
  },
  methods: {
    
    startTimer(){
      this.isTimerStarted = true;
        this.Timer = setInterval(()=>{
          this.fullTime++;
      }, 1000);
    },
    stopTimer(){
      this.isTimerStarted = false;
      clearInterval(this.Timer);
    },

    parseTime(){
      this.seconds = this.fullTime%60;
      this.minutes = Math.floor(this.fullTime/60)%60;
      this.hours = Math.floor(this.fullTime/60/60);
      this.parsedSeconds = this.parseTimeUnit(this.seconds);
      this.parsedMinutes = this.parseTimeUnit(this.minutes);
      this.parsedHours = this.parseTimeUnit(this.hours);
      this.parsedTime = `${this.parsedHours}:${this.parsedMinutes}:${this.parsedSeconds}`;
    },
    parseTimeUnit(timeUnit){
      if (timeUnit<10){
        return `0${timeUnit}`
      }
      return `${timeUnit}`
    },
    createLap(){
      if(this.isTimerStarted){
        let lap = {id: this.laps.length+1, h:this.hours, m:this.minutes, s:this.seconds};
        this.laps.push(lap);
      }
    }
  },

  mounted() {
    this.parseTime();
  },

  watch:{
    fullTime(){
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

.container{
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
}

.timer__inner{
  display: flex;
  min-height: 100vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.timer__body{
  height: 200px;
  width: 200px;
  border: 6px solid white;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  margin-bottom: 20px;
  font-size: 50px;
  color: white;
  font-family: Roboto;
}

.laps{
  width: 150px;
}

.lap{
  border-bottom: 1px white solid;
}

.timer__controls{
  display: flex;
  justify-content: space-between;
  width: 200px;
}

button{
  background: #4BA3C3;
  border: 2px solid #CCE6F4;
  border-radius: 15px;
  padding: 10px;
  cursor: pointer;
  font-size: 15px;
  color: #CCE6F4;
  transition: all .2s ease;
  font-family: Roboto;
}

button:hover{
  background: #CCE6F4;
  color: #4BA3C3;
}
</style>
