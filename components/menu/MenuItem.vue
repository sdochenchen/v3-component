<template>
  <li
    class="v3-menu-item"
    :class="{
      active: selectedKey === value,
      [mode]: true,
      disabled: disabled === true || disabled === 'true',
    }"
    @click="onClick"
  >
    <slot></slot>
  </li>
</template>
<script lang="ts">
import { inject } from "vue";

import {
  V3MenuMode,
  V3MenuParentKey,
  V3MenuSetRelationship,
  V3MenuSelectedKey,
  V3MenuSetSelectedKey,
} from "./Menu.vue";

export default {
  name: "v3-menu-item",
  props: {
    disabled: { type: [Boolean, String], default: false },
    value: { type: [Number, String], required: true },
  },
  setup(props) {
    const mode = inject(V3MenuMode);
    const parentKey = inject(V3MenuParentKey);

    const setRelationship = inject(V3MenuSetRelationship);
    const selectedKey = inject(V3MenuSelectedKey);
    const setSelectdKey = inject(V3MenuSetSelectedKey);

    setRelationship(props.value, parentKey);

    const onClick = () => {
      if (props.disabled === true || props.disabled === "true") {
        return;
      }

      if (selectedKey.value !== props.value) {
        setSelectdKey(props.value);
      }
    };

    return { mode, selectedKey, onClick };
  },
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-menu {
  &.horizontal {
    > .v3-menu-item {
      &.active {
        background-color: #fff;

        &::after {
          position: absolute;
          bottom: -1px;
          right: 0;
          left: 0;
          display: block;
          content: "";
          height: 2px;
          background-color: $v3-blue;
        }
      }
    }
  }
}

.v3-menu-item {
  color: $v3-main;
  cursor: pointer;
  transition: color $v3-transition, background-color $v3-transition;
  padding: 12px 24px;
  background-color: #fff;
  position: relative;
  white-space: nowrap;

  &:hover {
    color: $v3-blue-highlight;
  }

  &.active {
    color: $v3-blue;
    background-color: $v3-background-selected;
  }

  &.vertical {
    &.active {
      &::after {
        transform: scale(1);
      }
    }

    &::after {
      position: absolute;
      top: 0;
      bottom: 0;
      right: -1px;
      display: block;
      content: "";
      width: 2px;
      background-color: $v3-blue;
      transition: transform $v3-transition;
      transform: scale(0);
    }
  }

  &.disabled {
    color: $v3-disable;
    cursor: not-allowed;
  }
}
</style>
