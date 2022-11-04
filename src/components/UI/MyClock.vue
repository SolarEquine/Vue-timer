<template>
    <span>
        {{parsedTime}}
    </span>
</template>

<script>
    export default {
        name: "my-clock",
        props:{
            time:{
                type: Number,
                required: true,
            },
        },
        data(){
            return{
                milliseconds: 0,
                seconds: 0,
                minutes: 0,
                hours: 0,
                parsedMSeconds: '',
                parsedSeconds: '',
                parsedMinutes: '',
                parsedHours: '',
                parsedTime: '',
            }
        },
        methods: {
            parseTime(){
                this.milliseconds = this.time%100;
                this.seconds = Math.floor(this.time/1000)%60;
                this.minutes = Math.floor(this.time/1000/60)%60;
                this.hours = Math.floor(this.time/1000/60/60)%60;
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
      },
      mounted(){
        this.parseTime();
      },

      watch:{
        time(){
            this.parseTime();
        }
  }
    }
</script>

<style lang="scss" scoped>

</style>