<template>
  <div class="grid">
    <wrapper target=".grid" />
    
    <!-- Root -->
    <div class="col col-full">
      <node
        ref="root"
        class="root" 
        :isRoot="true"
        :id="0"
      >
        <template v-slot:content>
          Gamora vs. Hawkeye
        </template>
      </node>
    </div>

    <div class="col">
      <node
        ref="node1"
        side="left"
        :id="1"
        child="node2"
      >
        <template v-slot:content>
          Black Widow
        </template>

        <template v-slot:expand>
          <ul>
            <li>Expert tactician</li>
            <li>hand-to-hand combatant and secret agent</li>
            <li>Slowed aging and enhanced immune system</li>
            <li>Expert marksman and mastery of various other weapons</li>
          </ul>
        </template>
      </node>

      <node
        ref="node2"
        side="left"
        :id="2"
      >
        <template v-slot:content>
          Gamora
        </template>

        <template v-slot:expand>
          <ul>
            <li>Superhuman strength, speed, agility, and durability</li>
            <li>Skilled assassin</li>
            <li>Skilled hand-to-hand combatant</li>
          </ul>
        </template>
      </node>
    </div>

    <div class="col">
      <node
        ref="node3"
        side="right"
        :id="3"
        child="node2"
      >
        <template v-slot:content>
          Hawkeye
        </template>

        <template v-slot:expand>
          <ul>
            <li>Master Archer</li>
            <li>Expert Marksman, possesses very keen eyesight</li>
            <li>Master Martial Artist</li>
            <li>Weapons Proficiency</li>
          </ul>
        </template>
      </node>

      <node
        ref="node4"
        side="right"
        :id="4"
      >
        <template v-slot:content>
          Rocket
        </template>

        <template v-slot:expand>
          <ul>
            <li>Master tactician and field commander</li>
            <li>Skilled marksman and hand-to-hand combatant</li>
            <li>Genius-level intellect</li>
            <li>Normal-physical attributes of an Earth raccoon</li>
          </ul>
        </template>
      </node>
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

    .node {
      min-width: 150px;
      max-width: 150px;
      text-align: center;
    }
  }

</style>
