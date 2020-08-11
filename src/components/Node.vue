<template>
  <div
    class="node"
    :class="`node-${this.side} node${this.id}`"
  >
    <wrapper :target="`.node${this.id}`" />

    <template v-if="$slots.expand">
      <button 
        type="button"
        class="expand-button"
        @click="expand"
      />
    </template>

    <template v-if="!isRoot">
      <div 
        class="line-top"
        :style="{ 
          width: nodeWidth + 'px',
          height: topHeight + 'px',
          top: topPosition + 'px'
        }"
      >
        <div class="dot" />
      </div>
      <div 
        class="line-bottom"
        :style="{ 
          width: nodeWidth + 'px',
          height: bottomHeight + 'px',
          bottom: bottomPosition + 'px'
        }"            
      >
        <div class="arrow" />
      </div>
    </template>

    <div class="content">
      <slot name="content" />
    </div>

    <div
      class="expand-content"
      :class="{ 'expanded' : this.expanded }"
    >
      <slot name="expand" />
    </div>
  </div>
</template>

<script>

import Wrapper from './Wrapper.vue';

export default {
  name: 'Node',

  components: {
    Wrapper
  },

  props: {
    isRoot: {
      type: Boolean,
      default: false
    },
    id: {
      type: String,
      required: true
    },
    side: {
      type: String,
      default: 'left'
    }
  },

  data() {
    return {
      root: null,
      topHeight: null,
      bottomHeight: null,
      topPosition: null,
      bottomPosition: null,
      nodeWidth: null,
      expanded: false
    };
  },

  mounted() {
    if (!this.isRoot) {
      this.configureFlows();
      window.addEventListener("resize", this.handle);
    }
  },

  destroyed() {
    window.removeEventListener("resize", this.configureFlows());
  },

  methods: {
    handle() {
      this.configureFlows();
    },
    configureFlows() {
      this.root =  document.querySelector('.root');
      let rootH = this.root.offsetHeight; // height of root card with padding
      let rootW = this.root.offsetWidth; // width of root card with padding
      let rootY = this.root.getBoundingClientRect().top; // height from node to top of viewport
      let rootX = this.root.getBoundingClientRect().left; // height from left of viewport to node

      let nodeH = this.$el.offsetHeight; // height of root card with padding
      let nodeW = this.$el.offsetWidth; // height of root card with padding
      let nodeY = this.$el.getBoundingClientRect().top; // height from node to top of viewport
      let nodeX = this.$el.getBoundingClientRect().left; // hieght from left of viewport to node

      this.topHeight = nodeY - (rootY + rootH);
      // console.log(`(Top Height) ${this.topHeight} = (nY) ${nodeY} - ((rY) ${rootY} + (rH) ${rootH})`);

      this.bottomHeight = (nodeY + nodeH) - (rootY + rootH);
      // console.log(`(Bottom Height) ${this.bottomHeight} = ((nY) ${nodeY} + (nH) ${nodeH}) - ((rY) ${rootY} + (rH) ${rootH})`);


      let left = this.$el.classList.contains('node-left');
      if (left || this.side === 'left') {
        this.nodeWidth = rootX - (nodeX + nodeW);
        // console.log(`(Line Width) ${this.nodeWidth} = (rX) ${rootX} - ((nX) ${nodeX} + (nW) ${nodeW})`);
      }

      let right = this.$el.classList.contains('node-right');
      if (right || this.side === 'right') {
        this.nodeWidth = (nodeX) - (rootX + rootW);
        // console.log(`(Line Width) ${this.nodeWidth} = (nX) ${nodeX} - ((rX) ${rootX} + (nW) ${rootW})`);
      }
      
      let pad = 5;
      this.topPosition = pad - this.topHeight;
      this.bottomPosition = 0;
    },
    expand() {
      this.expanded = !this.expanded;
      setTimeout(() => {
        this.configureFlows();
      }, 1);
    }
  }
}
</script>

<style lang="scss" scoped>

  @import '@/assets/scss/core/all.scss';

  $node: #a3c4bc;
  $line: #413c58;
  $radius: 5px;

  .node {
    position: relative;
    width: max-content;
    background: $node;
    border: 1px solid $gray;
    padding: $pad;
    border-radius: 10px;
    box-shadow: 0 5px 10px rgba(0,0,0,0.4);

    margin-top: $pad*4; //temp
    
    &-right {
      align-self: flex-end;

      .line-top {
        position: absolute;
        right: calc(100% + 10px);
        border-bottom: 3px solid $line;
        border-left: 3px solid $line;
        border-bottom-left-radius: $radius*6;

        .dot {
          @include dot(10px, $line);
          position: absolute;
          bottom: -6px;
          right: 0;
        }
      }

      .line-bottom {
        position: absolute;
        right: calc(100% + 10px);
        border-bottom: 3px solid $line;
        border-left: 3px solid $line;
        border-bottom-left-radius: $radius*6;

        .arrow {
          @include arrow(5px, $line, 'right');
          position: absolute;
          right: 0;
          bottom: -6px;
        }
      }
    }

    &-left {
      align-self: flex-start;

      .line-top {
        position: absolute;
        left: calc(100% + 10px);
        border-bottom: 3px solid $line;
        border-right: 3px solid $line;
        border-bottom-right-radius: $radius*6;

        .dot {
          @include dot(10px, $line);
          position: absolute;
          bottom: -6px;
          left: 0;
        }
      }

      .line-bottom {
        position: absolute;
        left: calc(100% + 10px);
        border-bottom: 3px solid $line;
        border-right: 3px solid $line;
        border-bottom-right-radius: $radius*6;

        .arrow {
          @include arrow(5px, $line, 'left');
          position: absolute;
          left: 0;
          bottom: -6px;
        }
      }
    }

    .content {
      padding: $pad / 2;
    }

    .expand {
      &-button {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
      }

      &-content {
        visibility: hidden;
        height: 0;
        text-align: left;
        background: lightcyan;
        border-radius: $radius;

        ul {
          padding: $pad;
        }
      }
    }

    .expanded {
      visibility: visible;
      height: auto;
    }
  }

</style>
