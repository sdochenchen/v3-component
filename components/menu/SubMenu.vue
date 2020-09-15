<template>
  <li
    class="v3-sub-menu"
    :class="{
      active: openKeys.indexOf(value) > -1,
      selected,
      [mode]: true,
      disabled: disabled === true || disabled === 'true',
    }"
    v-click-outside="onOutside"
  >
    <div class="v3-sub-menu-title" @click="onClick">
      <slot name="title"></slot>
      <v3-icon
        v-if="showArrow === true || showArrow === 'true'"
        name="chevron-down"
        class="v3-sub-menu-icon"
        :size="12"
      ></v3-icon>
    </div>
    <v3-collapse-transition direction="vertical">
      <ul class="v3-sub-menu-list" v-show="openKeys.indexOf(value) > -1">
        <slot></slot>
      </ul>
    </v3-collapse-transition>
  </li>
</template>
<script lang="ts">
import { inject, provide, computed } from "vue";
import { Icon } from "v3-icons";

import { ClickOutside } from "../directives/ClickOutside";
import CollapseTransition from "../collapse-transition/CollapseTransition.vue";

import {
  V3MenuMode,
  V3MenuParentKey,
  V3MenuRelationship,
  V3MenuSelectedKey,
  V3MenuOpenKeys,
  V3MenuSetRelationship,
  V3MenuSetSelectedKey,
  V3MenuEnableOpenKey,
} from "./Menu.vue";

export default {
  name: "v3-sub-menu",
  components: {
    "v3-collapse-transition": CollapseTransition,
    "v3-icon": Icon,
  },
  directives: { "click-outside": ClickOutside },
  props: {
    disabled: { type: [Boolean, String], default: false },
    showArrow: { type: [Boolean, String], default: true },
    value: { type: [Number, String], required: true },
  },
  setup(props) {
    const mode = inject(V3MenuMode);
    const parentKey = inject(V3MenuParentKey);
    const relationship = inject(V3MenuRelationship);
    const selectedKey = inject(V3MenuSelectedKey);
    const openKeys = inject(V3MenuOpenKeys);

    const setRelationship = inject(V3MenuSetRelationship);
    const enableOpenKey = inject(V3MenuEnableOpenKey);

    setRelationship(props.value, parentKey);

    const calAncestors = () => {
      const ancestors: Array<string | number> = [];

      let current = selectedKey.value;

      while (current && relationship.value.has(current)) {
        const ancestor = relationship.value.get(current);

        if (ancestor !== "v3-menu-root") {
          ancestors.push(ancestor);
          current = ancestor;
        } else {
          current = "";
        }
      }

      return ancestors;
    };

    const selected = computed(() => {
      if (mode.value !== "horizontal") {
        return false;
      }

      if (!selectedKey.value) {
        return false;
      }

      const ancestors = calAncestors();

      return ancestors.indexOf(props.value) > -1;
    });

    const onClick = () => {
      if (props.disabled === true || props.disabled === "true") {
        return;
      }

      enableOpenKey(props.value, openKeys.value.indexOf(props.value) === -1);
    };
    const onOutside = () => {
      if (
        mode.value === "horizontal" &&
        openKeys.value.indexOf(props.value) > -1
      ) {
        enableOpenKey(props.value, false);
      }
    };

    provide(V3MenuParentKey, props.value);

    return { mode, openKeys, selected, onClick, onOutside };
  },
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-menu {
  > .v3-sub-menu {
    &.horizontal {
      &.active {
        > .v3-sub-menu-title {
          position: relative;

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

        > .v3-sub-menu-list {
          margin-top: 3px;
        }
      }

      &.selected {
        > .v3-sub-menu-title {
          position: relative;
          background-color: #fff;

          &::after {
            position: absolute;
            z-index: 1001;
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

    &.disabled {
      > .v3-sub-menu-title {
        color: $v3-disable;
        cursor: not-allowed;
      }
    }
  }
}

.v3-sub-menu {
  width: 100%;

  &.active {
    > .v3-sub-menu-title {
      color: $v3-blue;

      > .v3-sub-menu-icon {
        position: absolute;
        top: 50%;
        right: 8px;
        transform: translateY(-50%) rotateZ(-180deg);
      }
    }
  }

  &.horizontal {
    position: relative;

    > .v3-sub-menu-list {
      position: absolute;
      top: 100%;
      left: 0;
      z-index: 1000;
      width: 100%;
      box-shadow: 0px 4px 4px rgba(0, 0, 0, 0.23921568627451);
    }
  }

  &.disabled {
    > .v3-sub-menu-title {
      color: $v3-disable;
      cursor: not-allowed;
    }
  }

  > .v3-sub-menu-title {
    padding: 12px 24px;
    color: $v3-main;
    cursor: pointer;
    transition: color $v3-transition;
    position: relative;

    &:hover {
      color: $v3-blue-highlight;
    }

    > .v3-sub-menu-icon {
      position: absolute;
      top: 50%;
      right: 8px;
      transition: transform $v3-transition;
      transform: translateY(-50%) rotateZ(0);
    }
  }

  > .v3-sub-menu-list {
    list-style: none;
    margin-bottom: 0;

    .v3-menu-item {
      padding: 12px 24px 12px 48px;
    }
  }
}
</style>
