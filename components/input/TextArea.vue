<template>
  <textarea
    class="v3-text-area"
    :class="{
      autosize: autosize === true || autosize === 'true',
      bordered: bordered === true || bordered === 'true',
      error: error === true || error === 'true',
      disabled: disabled === true || disabled === 'true',
    }"
    :disabled="disabled === true || disabled === 'true'"
    ref="el"
    :value="value"
    @input="onInput"
  />
</template>
<script lang="ts">
import { ref, onMounted } from "vue";

import { calNodeHeight } from "../utils/calNodeHeight";

export default {
  name: "v3-text-area",
  props: {
    autosize: { type: [Boolean, String], default: true },
    bordered: { type: [Boolean, String], default: true },
    disabled: [Boolean, String],
    error: [Boolean, String],
    value: String,
  },
  setup(props, context) {
    const el = ref<HTMLTextAreaElement>(null);
    const originHeight = ref(0);

    onMounted(() => {
      if (el.value) {
        const { top, bottom } = el.value.getBoundingClientRect();
        originHeight.value = bottom - top;
      }
    });

    const onInput = (ev: InputEvent) => {
      context.emit("update:value", (ev.target as HTMLTextAreaElement).value);

      if (props.autosize && el.value) {
        const hiddenHeight = calNodeHeight(el.value);
        if (hiddenHeight > originHeight.value) {
          el.value.style.height = hiddenHeight + "px";
        }
      }
    };

    return { onInput, el };
  },
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-text-area {
  color: $v3-main;
  font-size: 14px;
  padding: 4px 12px;
  border: none;
  border-radius: 2px;
  color: inherit;
  transition: border-color $v3-transition;
  text-overflow: ellipsis;

  &.disabled {
    color: $v3-secondary;

    border-color: $v3-disable;
    background-color: $v3-background-disable;
    cursor: not-allowed;

    &:hover {
      border-color: $v3-disable;
    }
  }

  &.error {
    color: $v3-red;
    border-color: $v3-red;
    box-shadow: 0px 0px 2px $v3-red-highlight;

    &:hover {
      border-color: $v3-red;
    }

    &:focus {
      border-color: $v3-red;
      box-shadow: 0px 0px 2px $v3-red-highlight;
    }
  }

  &.bordered {
    border: 1px solid;
    border-color: $v3-border;
  }

  &::placeholder {
    color: $v3-disable;
  }

  &::selection {
    color: #fff;
    background-color: $v3-blue;
  }

  &:hover {
    border-color: $v3-blue-highlight;
  }

  &:focus {
    border-color: $v3-blue;
    box-shadow: 0px 0px 2px $v3-blue-highlight;
    outline: none;
  }

  &.autosize {
    resize: none;
    overflow-y: hidden;
  }
}
</style>
