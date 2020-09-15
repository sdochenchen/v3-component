<template>
  <li
    class="v3-select-option"
    :class="{
      active: selectValue === value,
      disabled: disabled === true || disabled === 'true',
    }"
    @click="onClick"
  >
    {{ label || value }}
  </li>
</template>
<script lang="ts">
import { inject } from "vue";

import { V3SelectValue, V3UpdateSelectValue } from "./Select.vue";

export default {
  name: "v3-option",
  components: {},
  props: {
    disabled: [Boolean, String],
    label: [Number, String],
    value: { type: [Number, String], required: true },
  },
  setup(props, context) {
    const selectValue = inject(V3SelectValue);
    const updateSelectValue = inject(V3UpdateSelectValue);

    const onClick = (ev: MouseEvent) => {
      if (props.disabled === true || props.disabled === "true") {
        ev.preventDefault();

        return;
      }

      updateSelectValue(props.value);
    };

    return { selectValue, onClick };
  },
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-select-option {
  width: 100%;
  padding: 8px 12px;
  overflow: hidden;
  text-overflow: ellipsis;
  font-size: 14px;
  color: $v3-main;
  cursor: pointer;
  background-color: #fff;
  transition: background-color $v3-transition, color $v3-transition;

  &:hover {
    background-color: $v3-background-hover;
  }

  &.active {
    color: $v3-blue;
  }

  &.disabled {
    color: $v3-disable;
    background-color: #fff;
    cursor: not-allowed;
  }
}
</style>
