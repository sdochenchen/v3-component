<template>
  <button
    v-if="!href"
    class="v3-button"
    :class="{
      danger: danger === true || danger === 'true',
      disabled: disabled === true || disabled === 'true',
      loading: loading === true || loading === 'true',
      [size]: true,
      [type]: true,
    }"
    :disabled="disabled === true || disabled === 'true'"
    :type="htmlType"
  >
    <v3-icon
      v-if="iconName && !loading"
      :name="iconName"
      :size="iconSize"
      :style="{ marginRight: '4px' }"
    ></v3-icon>
    <v3-icon
      v-if="loading === true || loading === 'true'"
      name="loading"
      :size="iconSize"
      :spinning="true"
      :style="{ marginRight: '4px' }"
    ></v3-icon>
    <span><slot></slot></span>
  </button>
  <a
    v-else
    class="v3-href"
    :class="{
      disabled: disabled === true || disabled === 'true',
    }"
    :href="disabled ? 'javascript:void(0);' : href"
    :target="target"
    @click="onClick"
  >
    <span><slot></slot></span>
  </a>
</template>
<script lang="ts">
import { Icon } from "v3-icons";

export default {
  name: "v3-button",
  components: { "v3-icon": Icon },
  props: {
    danger: [Boolean, String],
    disabled: [Boolean, String],
    href: String,
    htmlType: { type: String, default: "button" },
    iconName: String,
    iconSize: { type: [Number, String], default: "1em" },
    loading: [Boolean, String],
    size: {
      type: String,
      default: "middle",
      validator<String>(val: string) {
        return ["small", "middle", "large"].includes(val);
      },
    },
    target: String,
    type: {
      type: String,
      default: "default",
      validator<String>(val: string) {
        return ["primary", "default"].includes(val);
      },
    },
  },
  setup(props, context) {
    const onClick = (ev: MouseEvent) => {
      if (props.disabled) {
        ev.preventDefault();
      }
    };

    return { onClick };
  },
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-button {
  height: 32px;
  padding: 0 8px;
  display: inline-flex;
  justify-content: flex-start;
  align-items: center;
  border-radius: 2px;
  background-color: #fff;
  outline: none;
  border: 1px solid;
  border-color: $v3-border;
  color: $v3-main;
  cursor: pointer;
  font-size: 14px;
  transition: color $v3-transition, background-color $v3-transition,
    border-color $v3-transition;

  &:hover {
    color: $v3-blue-highlight;
    border-color: $v3-blue-highlight;
  }

  &.primary {
    background-color: $v3-blue;
    border-color: $v3-blue;
    color: #fff;

    &:hover {
      background-color: $v3-blue-highlight;
      border-color: $v3-blue-highlight;
    }
  }

  &.danger {
    color: $v3-red;
    border-color: $v3-red;

    &:hover {
      color: $v3-red-highlight;
      border-color: $v3-red-highlight;
    }

    &.primary {
      background-color: $v3-red;
      color: #fff;

      &:hover {
        background-color: $v3-red-highlight;
        border-color: $v3-red-highlight;
      }
    }
  }

  &.disabled {
    cursor: not-allowed;
    color: $v3-disable;
    border-color: $v3-disable;

    &:hover {
      color: $v3-disable;
      border-color: $v3-disable;
    }

    &.primary {
      background-color: $v3-background-disable;
      border-color: $v3-disable;
      color: $v3-disable;

      &:hover {
        background-color: $v3-background-disable;
        border-color: $v3-disable;
      }
    }
  }

  &.small {
    height: 24px;
  }

  &.large {
    height: 40px;
    font-size: 16px;
  }
}

.v3-href {
  display: inline-block;
  padding: 0 8px;
  color: $v3-blue;
  cursor: pointer;
  font-size: 14px;
  text-decoration: none;
  transition: color $v3-transition;

  &:hover {
    color: $v3-blue-highlight;
  }

  &.disabled {
    cursor: not-allowed;
    color: $v3-disable;

    &:hover {
      color: $v3-disable;
    }
  }
}
</style>
