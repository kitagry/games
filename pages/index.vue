<template lang="pug">
div
  card(v-for="content in contents", :content="content")
</template>


<script>
import Card from './../components/Card.vue';

var marks = ["♠", "♥", "♣", "◆"]
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
var contents = [];
for(var i = 0; i < marks.length; i++) {
  for(var j = 0; j < numbers.length; j++) {
    contents.push({"mark": marks[i], "number": numbers[j], "index": marks[i]+numbers[j]})
  }
}

export default {
  components: {
    Card,
  },
  data: function(){
    return {
      contents: contents
    }
  }
}
</script>

<style lang="sass">
</style>