<template>
    <div class="laps">
    <div
        v-for="lap in laps.slice().reverse()"
        :key="lap.id"
        class="lap"><span>{{lap.id}}: <my-clock :time="lap.lapTime"/></span> <span style="color: gray">
            +<my-clock :time="lap.delta"/>
        </span></div>
    </div>
</template>

<script>
    export default {
        props:{
            laps: {
                type: Array,
                required: true,
        },
        },
    }
</script>

<style scoped>
.laps{
  width: 300px;
}

.lap{
  border-bottom: 1px white solid;
  margin-top: 15px;
  color:white;
  font-family: Roboto;
  display: flex;
  justify-content: space-between;
}
</style>