<template>
  <ul class="v3-menu" :class="{ [mode]: true }">
    <slot></slot>
  </ul>
</template>
<script lang="ts">
import { InjectionKey, provide, ref, Ref, computed, readonly } from "vue";

export const V3MenuParentKey: InjectionKey<string | number> = Symbol(
  "V3MenuParentKey"
);
export const V3MenuRelationship: InjectionKey<Ref<
  Map<string | number, string | number>
>> = Symbol("V3MenuRelationship");
export const V3MenuMode: InjectionKey<Ref<string>> = Symbol("V3MenuMode");
export const V3MenuSelectedKey: InjectionKey<Ref<string | number>> = Symbol(
  "V3MenuSelectedKey"
);
export const V3MenuOpenKeys: InjectionKey<Ref<
  Array<string | number>
>> = Symbol("V3MenuOpenKeys");

export const V3MenuSetRelationship: InjectionKey<(
  key: string | number,
  parentKey: string | number
) => void> = Symbol("V3MenuSetRelationship");
export const V3MenuSetSelectedKey: InjectionKey<(
  key: string | number
) => void> = Symbol("V3MenuSetSelectedKey");
export const V3MenuEnableOpenKey: InjectionKey<(
  key: string | number,
  enabled: boolean
) => void> = Symbol("V3MenuEnableOpenKey");

export default {
  name: "v3-menu",
  props: {
    defaultSelectedKey: [String, Number],
    defaultOpenKeys: Array,
    mode: {
      type: String,
      default: "vertical",
      validator<String>(val: string) {
        return ["vertical", "horizontal"].includes(val);
      },
    },
    openKeys: Array,
    selectedKey: [String, Number],
  },
  setup(props, context) {
    const menuMode = computed(() => props.mode);

    const selected = ref<string | number>(props.defaultSelectedKey);
    const opened = ref<Array<string | number>>(
      (props.defaultOpenKeys as Array<string | number>) || []
    );

    const menuSelectedKey = computed(() => {
      if (props.selectedKey !== undefined) {
        return props.selectedKey;
      }

      return selected.value;
    });
    const menuOpenKeys = computed(() => {
      if (props.openKeys !== undefined) {
        return props.openKeys as Array<string | number>;
      }

      return opened.value;
    });

    const relationship = ref(new Map<string | number, string | number>());

    const setRelationship = (
      key: string | number,
      parentKey: string | number
    ) => {
      relationship.value.set(key, parentKey);
    };

    const setSelectedKey = (key: string | number) => {
      selected.value = key;
      context.emit("update:selected-key", key);
      context.emit("select", menuSelectedKey.value);

      if (props.mode === "horizontal" && menuOpenKeys.value.length) {
        opened.value = [];

        context.emit("update:open-keys", []);
        context.emit("open-change", []);
      }
    };
    const enableOpenKey = (key: string | number, enabled: boolean) => {
      if (enabled) {
        if (opened.value.indexOf(key) === -1) {
          opened.value.push(key);
        }
      } else {
        opened.value = opened.value.filter((i) => i !== key);
      }

      context.emit("update:open-keys", [...menuOpenKeys.value]);
      context.emit("open-change", [...menuOpenKeys.value]);
    };

    provide(V3MenuParentKey, "v3-menu-root");
    provide(V3MenuRelationship, relationship);
    provide(V3MenuMode, readonly(menuMode));
    provide(V3MenuSelectedKey, menuSelectedKey);
    provide(V3MenuOpenKeys, menuOpenKeys);

    provide(V3MenuSetRelationship, setRelationship);
    provide(V3MenuSetSelectedKey, setSelectedKey);
    provide(V3MenuEnableOpenKey, enableOpenKey);
  },
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-menu {
  list-style: none;
  margin-bottom: 0;
  font-size: 14px;
  border-right: 1px solid $v3-border;

  &.horizontal {
    display: flex;
    justify-content: flex-start;
    align-items: center;
    border-right: none;
    border-bottom: 1px solid $v3-border;
  }
}
</style>
