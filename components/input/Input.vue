<template>
  <label
    class="v3-input"
    :class="{
      bordered: bordered === true || bordered === 'true',
      error: error === true || error === 'true',
      disabled: disabled === true || disabled === 'true',
      prefix: !!prefixIconName,
      suffix: !!suffixIconName,
      [type]: true,
      [size]: true,
    }"
    v-bind="labelAttrs"
  >
    <v3-icon
      v-if="prefixIconName"
      class="v3-input-prefix-icon"
      :name="prefixIconName"
      size="1em"
      :style="prefixIconStyle"
      @click="onPrefixIcon"
    ></v3-icon>
    <input
      class="v3-input-el"
      :class="{
        bordered: bordered === true || bordered === 'true',
        error: error === true || error === 'true',
        disabled: disabled === true || disabled === 'true',
        prefix: !!prefixIconName,
        suffix: !!suffixIconName,
        [type]: true,
        [size]: true,
      }"
      :value="value"
      :checked="checked"
      :disabled="disabled === true || disabled === 'true'"
      :readonly="readonly === true || readonly === 'true'"
      :type="type"
      @input="onInput"
      v-bind="$attrs"
    />
    <v3-icon
      v-if="suffixIconName"
      class="v3-input-suffix-icon"
      :name="suffixIconName"
      size="1em"
      :style="suffixIconStyle"
      @click="onSuffixIcon"
    ></v3-icon>
  </label>
</template>
<script lang="ts">
import { computed, watchEffect } from "vue";
import { Icon } from "v3-icons";

export default {
  name: "v3-input",
  components: { "v3-icon": Icon },
  inheritAttrs: false,
  props: {
    bordered: { type: [Boolean, String], default: true },
    checked: { type: Boolean, default: false },
    disabled: [Boolean, String],
    error: [Boolean, String],
    labelAttrs: Object,
    prefixIconName: String,
    prefixIconStyle: [String, Object],
    readonly: [Boolean, String],
    suffixIconName: String,
    suffixIconStyle: [String, Object],
    size: {
      type: String,
      default: "middle",
      validator<String>(val: string) {
        return ["small", "middle", "large"].includes(val);
      },
    },
    type: { type: String, defult: "text" },
    value: String,
  },
  setup(props, context) {
    const onInput = (ev: InputEvent) => {
      context.emit("update:value", (ev.target as HTMLInputElement).value);
      context.emit("update:checked", (ev.target as HTMLInputElement).checked);
    };

    const onPrefixIcon = (ev: MouseEvent) => {
      context.emit("click-prefix", ev);
    };

    const onSuffixIcon = (ev: MouseEvent) => {
      context.emit("click-suffix", ev);
    };

    return { onInput, onPrefixIcon, onSuffixIcon };
  },
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-input {
  display: inline-block;
  position: relative;
  height: 32px;
  color: $v3-main;
  font-size: 14px;

  &.bordered {
    > .v3-input-el {
      border: 1px solid;
      border-color: $v3-border;
    }
  }

  &.disabled {
    color: $v3-secondary;

    > .v3-input-el {
      border-color: $v3-disable;
      background-color: $v3-background-disable;
      cursor: not-allowed;

      &:hover {
        border-color: $v3-disable;
      }
    }
  }

  &.error {
    color: $v3-red;

    > .v3-input-el {
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
  }

  &.small {
    height: 24px;
  }

  &.large {
    height: 40px;
    font-size: 16px;
  }

  &.prefix {
    > .v3-input-el {
      padding-left: 28px;
    }
  }

  &.suffix {
    > .v3-input-el {
      padding-right: 28px;
    }
  }

  &.radio {
    width: 32px;
    height: 32px;
    display: inline-flex;
    justify-content: center;
    align-items: center;

    &.small {
      width: 24px;
      height: 24px;
    }

    &.large {
      width: 40px;
      height: 40px;
      font-size: 16px;
    }

    > .v3-input-el {
      width: 16px;
      height: 16px;
      padding: 0;

      &:focus {
        box-shadow: none;
      }
    }
  }

  &.range {
    > .v3-input-el {
      padding: 0;
    }
  }

  > .v3-input-prefix-icon {
    position: absolute;
    left: 8px;
    top: 50%;
    transform: translateY(-50%);
    color: inherit;
  }

  > .v3-input-el {
    width: 100%;
    height: 100%;
    padding: 0 12px;
    border: none;
    border-radius: 2px;
    color: inherit;
    font-size: inherit;
    transition: border-color $v3-transition;
    text-overflow: ellipsis;
    outline: none;

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
    }
  }

  > .v3-input-suffix-icon {
    position: absolute;
    right: 8px;
    top: 50%;
    transform: translateY(-50%);
    color: inherit;
  }
}
</style>
