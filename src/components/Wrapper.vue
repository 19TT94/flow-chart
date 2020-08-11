<template>
  <div class="wrapper">
    <div class="wrapper-info">
      <ul class="wrapper-info-content">
        <li>height: {{ height }}</li>
        <li>width: {{ width }}</li>
        <li>x: {{ x }}</li>
        <li>y: {{ y }}</li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Wrapper',

  props: {
    target: {
      type: String,
      required: true
    }
  },

  data() {
    return {
      height: 0,
      width: 0,
      x: 0,
      y: 0,
    };
  },

  mounted() {
    let offsetX = 0;
    let offsetY = 0;

    let elem = document.querySelector(this.target);
    let box = elem.getBoundingClientRect();

    this.height = elem.offsetHeight;
    this.width = elem.offsetWidth;
    this.x = box.x - offsetX;
    this.y = box.y - offsetY;
  }
}
</script>

<style lang="scss" scoped>

  @import '@/assets/scss/core/all.scss';

  $dot: #413c58;
  $info: #f2e7c9;

  .wrapper {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;

    &-info {
      top: 0;
      left: 0;
      width: $pad/2;
      height: $pad/2;
      border-radius: 50%;
      background: $dot;
      margin: $pad/2;

      &-content {
        position: absolute;
        top: $pad*3;
        width: max-content;
        transition: all ease 0.5s;
        background: $info;
        border-radius: $pad;
        opacity: 0.6;
        padding: $pad;
        visibility: hidden;  
        transition: all ease 1;
        z-index: z('top');
      }

      &:hover {
        .wrapper-info-content {
          opacity: 1;
          visibility: visible;
        }  
      }
    }
  }

</style>
