<template>
  <div class="grid">
    <wrapper target=".grid" />
    
    <!-- Root -->
    <div class="col col-full">
      <node
        class="root" 
        :isRoot="true"
        id="0"
      >
        <template v-slot:content>
          Root Node
        </template>
      </node>
    </div>

    <div class="col">
      <node
        side="left"
        id="1"
      >
        <template v-slot:content>
          Node 1
        </template>
      </node>

      <node
        side="left"
        id="2"
      >
        <template v-slot:content>
          Node 2
        </template>
      </node>
    </div>

    <div class="col">
      <node
        side="right"
        id="3"
      >
        <template v-slot:content>
          Node 3
        </template>
      </node>

      <!-- <node
        side="right"
        id="4"
      >
        <template v-slot:content>
          Node 4
        </template>
      </node> -->
    </div>

  </div>
</template>

<script>

import Wrapper from './Wrapper.vue';
import Node from './Node.vue';

export default {
  name: 'Grid',

  components: {
    Wrapper,
    Node
  }
}
</script>

<style lang="scss" scoped>

  @import '@/assets/scss/core/all.scss';

  $grid: #e7efc5;

  .grid {
    position: relative;
    width: 100%;
    background: $grid;
    border: 1px solid $gray;
    padding: $pad;
    @include flexbox(row, wrap, center, flex-start);

    .root {
      align-self: center;
      min-width: 100px;
      text-align: center;
      margin: 0;
    }

    .col {
      width: 50%;
      display: flex;
      flex-direction: column;

      &-full {
        width: 100%;
      }
    }
  }

</style>
