<template lang="pug">
  .nav_circle(@wheel="rotating" :style="doRotate")
    item-nav.item_nav_wrap(
      v-for="(item, i) in nav"
      :key="i"
      :bgImg="item.img"
      :setRotate="angle * i"
      :setSkew="90 - angle"
      :newRotateImg="newRotate"
    )
</template>

<script>
// можно настроить ещё гибче,
// чтоб адекватнее выглядело при 1-3-х пунктов меню
//
// P.S.: отлавливаю баг,
// который появлется при rotate против часовой стрелки у некоторых картинок пунктов меню
//
import ItemNav from "../components/ItemNav.vue";
// img
import NavImg1 from "../assets/img/1.png";
import NavImg2 from "../assets/img/2.png";
import NavImg3 from "../assets/img/3.png";
import NavImg4 from "../assets/img/4.png";
import NavImg5 from "../assets/img/5.png";
import NavImg6 from "../assets/img/6.png";
import NavImg7 from "../assets/img/7.png";
import NavImg8 from "../assets/img/8.png";

export default {
  components: {
    ItemNav
  },
  data() {
    return {
      nav: [
        { img: NavImg1 },
        { img: NavImg2 },
        { img: NavImg3 },
        { img: NavImg4 },
        { img: NavImg5 },
        { img: NavImg6 },
        { img: NavImg7 },
        { img: NavImg8 }
      ],
      newRotate: 0,
      itemHover: null
    };
  },
  computed: {
    angle() {
      return Math.floor(360 / this.nav.length);
    },
    doRotate() {
      return {
        transform: `rotate(${this.newRotate}deg)`
      };
    }
  },
  methods: {
    rotating(e) {
      let timer;
      if (e.wheelDelta >= 0) {
        timer = setTimeout(() => {
          this.newRotate -= this.angle;
        }, 4);
      } else {
        clearTimeout(timer);
        timer = setTimeout(() => {
          this.newRotate += this.angle;
        }, 4);
      }
    }
  }
};
</script>

<style lang="postcss" scoped>
.nav_circle {
  height: 100%;
  width: 100%;
  position: relative;
  transition: transform 1s linear;
}
</style>
