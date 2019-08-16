<template lang="pug">
  .item_nav(:style="setStyleNav")
    .img_nav(:style="[{'background-image': `url(${this.bgImg})`}, setImgNav]")
</template>

<script>
export default {
  props: {
    bgImg: {
      type: String,
      required: true
    },
    setRotate: {
      type: Number,
      required: true
    },
    newRotateImg: {
      type: Number,
      required: true
    },
    setSkew: {
      type: Number,
      required: true
    }
  },
  computed: {
    setStyleNav() {
      return {
        transform: `rotate(${this.setRotate}deg) skew(${this.setSkew}deg)`
      };
    },
    setImgNav() {
      return {
        transform: `skew(-${this.setSkew}deg) rotate(${this.imgRotating}deg)`
      };
    },
    imgRotating() {
      return `-${this.setRotate + this.newRotateImg}`;
    }
  }
};
</script>

<style lang="postcss" scoped>
.item_nav {
  height: 100%;
  width: 100%;
  position: absolute;
  left: -50%;
  top: -50%;
  transform-origin: 100% 100%;
  cursor: pointer;
  border: 1px solid lightgrey;
  transition: background-color 0.5s linear;
  &:hover {
    background-color: lightgrey;
  }
}

.img_nav {
  background-repeat: no-repeat;
  background-position: center;
  background-size: contain;
  height: 25px;
  width: 25px;
  position: absolute;
  bottom: 25px;
  right: 35px;
  transition: transform 1s linear;
}
</style>
