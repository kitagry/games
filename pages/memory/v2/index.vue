<template lang="pug">
div
  transition-group(tag="div", name="card-list", @before-enter="beforeEnter",
      @after-enter="afterEnter",
      @enter-cancelled="afterEnter",
      @after-leave="afterLeave",
      appear)
    card(v-for="(content, idx) in contents", :content="content", :key="content.key", :data-index="idx", @open-card="openCard")
  congratulations(:show="showCongratulations")
</template>

<script>
import Vue from 'vue';
import _ from 'lodash';
import Card from './../../../components/Card.vue';
import Congratulations from './../../../components/Congratulations.vue';

var marks = ["♠", "♥"];
var numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
// var numbers = [1, 1];

export default {
  components: {
    Card,
    Congratulations,
  },
  data: function(){
    return {
      contents: [],
      previousIndex: null,
      showCongratulations: false,
    }
  },
  methods: {
    // enter の初めにインデックス×100でディレイを付ける
    beforeEnter(el) {
      el.style.transitionDelay = 100 * el.dataset.index + 'ms';
    },
    // enter が終わるか中止されたらディレイを消す
    afterEnter(el) {
      el.style.transitionDelay = '';
      this.contents[el.dataset.index]["show"] = false;
      if (el.dataset.index == this.contents.length - 1) {
        this.contents = _.shuffle(this.contents);
      }
    },
    afterLeave(el) {
      this.showCongratulations = true;
    },
    openCard(key) {
      console.log(key);
      var index = this.contents.findIndex(function(element){
        return element.key === key;
      });
      if (this.contents[this.previousIndex] == null) {
        this.previousIndex = index;
      } else {
        this.$nextTick(function(){
          this.sleep(500);
          if (this.contents[this.previousIndex].number == this.contents[index].number) {
            if (this.unopenCards == 0) {
              this.contents = [];
            }
          } else {
            this.contents[index].show = false;
            this.contents[this.previousIndex].show = false;
          }
          this.previousIndex = null;
        })
      }
    },
    sleep(time) {
      const d1 = new Date();
      while (true) {
          const d2 = new Date();
          if (d2 - d1 > time) {
              return;
          }
      }
    }
  },
  computed: {
    unopenCards: function() {
      var unopenCards = this.contents.filter(function(element){
        return element.show == false;
      });
      return unopenCards.length;
    }
  },
  created() {
    for(var j = 0; j < numbers.length; j++) {
      for(var i = 0; i < marks.length; i++) {
        this.contents.push({"mark": marks[i], "number": numbers[j], "key": marks[i]+numbers[j], "show": true});
      }
    }
  }
}
</script>

<style lang="sass">
.card-list-enter-active, .card-list-leave-active
  transition: transform 1s, opacity 1s, filter 1s;
.card-list-move:not(.card-list-leave-active)
  transition: transform 1s;
.card-list-enter
  opacity: 0;
  filter: blur(5px);
.card-list-leave-to
  opacity: 0;
  transform: translateY(600px) rotate(540deg);
</style>