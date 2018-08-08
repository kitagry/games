<template lang="pug">
div
  transition(name="rotate", mode="out-in")
    .card(@click="orientation = !orientation", v-if="orientation", key="table")
      .card-front(:style="{'color': (content.mark == '♠' || content.mark == '♣' ? 'black' : 'red')}")
        span {{content.number}}{{content.mark}}
        | {{content.mark}}
        span {{content.number}}{{content.mark}}
    .card(@click="orientation = !orientation", v-else, key="back")
      .card-back
</template>


<script>
export default {
  props: ["content"],
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

.rotate-enter, .rotate-leave-to
  transition-duration: 0.5s;
  transform: rotateY(90deg);
.rotate-enter-to, .rotate-leave
  transition-duration: 0.5s;
  transform: rotateY(0deg);

</style>