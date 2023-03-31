<template>
  <div class="container">
    <a
      class="bubble bubble-link"
      :href="link"
      v-if="link"
      :aria-label="header"
      target="_blank"
    >
      <slot></slot>
    </a>
    <div class="bubble" :aria-label="header" v-else>
      <slot></slot>
    </div>
    <p v-if="content" class="text">{{ content }}</p>
  </div>
</template>

<script>
import Vue from 'vue';
import Component from 'vue-class-component';

@Component({
  props: {
    link: {
      type: String,
      required: false,
      default: ''
    },
    content: {
      type: String,
      required: false,
      defaultValue: ''
    },
    header: {
      type: String,
      default: false
    }
  }
})
export default class SocialMediaBubble extends Vue {}
</script>

<style lang="scss">
.container {
  height: 36px;
  padding: 0;
}

.bubble {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  color: #fefefe;
  font-size: 1.2rem;
  line-height: 26px;
  height: 36px;
  width: 36px;
  align-items: center;
  justify-content: center;
  padding: 4px;

  &.bubble-link:hover,
  &.bubble-link:focus {
    background-color: #fefefe;
    color: #000;
    border-radius: 50%;
    text-decoration: none;
  }

  .content {
    margin: 3px;
  }

  .text {
    margin: 2px;
  }
}
</style>
