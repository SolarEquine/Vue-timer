<template>
    <div class="laps">
    <div
        v-for="lap in laps.slice().reverse()"
        :key="lap.id"
        class="lap">{{lap.id}}: {{lap.h}}:{{lap.m}}:{{lap.s}}:{{lap.ms}}</div>
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
  margin-bottom: 10px;
  color:white;
  font-family: Roboto;
}
</style>