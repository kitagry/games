<template lang="pug">
div
  transition(name="last-text"
    mode="out-in"
    v-on:before-enter="beforeEnter"
    v-on:enter="enter"
    v-on:after-enter="afterEnter"
    v-on:leave="leave")
    h1.last-text(v-if="show && cong", key="congratulations") Congratulations!!!!
    h1.last-text(v-if="show && !cong", key="play") Let's play again next time!!! 
</template>
  
<script>
export default {
  head () {
    return {
      script: [
        { src: 'https://cdnjs.cloudflare.com/ajax/libs/velocity/1.2.3/velocity.min.js' }
      ],
      link: [
        { rel: 'stylesheet', href: 'https://fonts.googleapis.com/css?family=Homemade+Apple' }
      ]
    } 
  },
  props: ["show"],
  data: function() {
    return {
      cong: true,
    }
  },
  methods: {
    beforeEnter: function (el) {
      el.style.opacity = 0
    },
    enter: function (el, done) {
      Velocity(el, { opacity: 1, fontSize: '5.4em' }, { duration: 300 })
      Velocity(el, { fontSize: '5em' }, { complete: done })
    },
    afterEnter: function(el) {
      if (this.cong) {
        this.cong = false;
      } else {
        console.log("Change Color!");
        Velocity(el, { color: "#F2B9A1" }, { duration: 300 })
      }
    },
    leave: function (el, done) {
      Velocity(el, { translateX: '15px', rotateZ: '50deg' }, { duration: 600 })
      Velocity(el, { rotateZ: '70deg' }, { loop: 2 })
      Velocity(el, {
        rotateZ: '45deg',
        translateY: '1000px',
        translateX: '30px',
        opacity: 0
      }, { complete: done })
    }
  }
}
</script>

<style lang="sass">
.last-text
  margin-top: 200px;
  text-align: center;
  font-size: 5em;
  font-family: 'Homemade Apple', cursive; 
</style>