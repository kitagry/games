<template lang="pug">
.card(@click="orientation = !orientation")
  .card-front
    span 7♣
    | ♣
    span 7♣
  .card-back(v-show="orientation")
</template>


<script>
export default {
  data: function(){
    return {
      orientation: false,
    }
  }
}
</script>

<style lang="sass">
.card 
  display: inline-block;
  width: 176px;
  height: 246px;
  margin: 20px;
  cursor: pointer;
  div
    position: absolute;
    width: 160px;
    height: 230px;
    font-size: 2em;
    text-align: center;
    line-height: 230px;
    color: #000;
    background-color: #fff;
    border: 8px solid #fff;
    border-radius: 5px;
    box-shadow: 2px 2px 5px rgba(0,0,0,0.5);
    span
      position: absolute;
      left: 0;
      top: 0;
      font-size: 0.5em;
      width: auto;
      line-height: 1em;
    span:last-child
      left: auto;
      top: auto;
      right: 0;
      bottom: 0;
      transform: rotate(180deg);
  .card-back
    background: #36c;
</style>