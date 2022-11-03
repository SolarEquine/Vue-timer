<template>
  <div class="timer__inner">
    <div class="timer__margin"></div>
    <div class="timer__body">
      {{ timeDelta }}
    </div>
    <div class="timer__controls">
      <button @click="$emit('start')">Старт</button>
      <button @click="$emit('stop')">Стоп</button>
      <button @click="$emit('lap')">Круг</button>
    </div>
    <div class="timer__laps">
      <timer-laps
      :laps="laps"
      />
    </div>
  </div>
</template>

<script>
import TimerLaps from "@/components/TimerLaps";


export default {
  components: {
    TimerLaps,
  },
      props: {
        laps: {
          type: Array,
          required: true,
        },
        timeDelta: {
          type: String,
          required: true,
        }
      },
        
    }
</script>

<style scoped>


.timer__inner{
  display: flex;
  min-height: 100vh;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.timer__margin{
  min-height: 30vh;
}

.timer__body{
  height: 300px;
  width: 300px;
  margin-top: 20px;
  border: 10px solid white;
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 50%;
  margin-bottom: 20px;
  font-size: 50px;
  color: white;
  font-family: Roboto;
}

.timer__laps{
  flex: 1 1 0;
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

@media (max-width: 400px){
  .timer__body{
  height: 200px;
  width: 200px;
  font-size: 30px;
  }

  .laps{
    width: 200px;
  }
}

</style>