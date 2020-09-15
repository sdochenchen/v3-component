<template>
  <div class="v3-tabs" :class="{ [tabPosition]: true }">
    <TabNav
      :active-tab-label-rect="activeTabLabelRect"
      :render-labels="renderLabels"
      :tab-position="tabPosition"
      :type="type"
    />
    <div class="v3-tabs-content" :style="contentStyle">
      <slot></slot>
    </div>
  </div>
</template>
<script lang="ts">
import { InjectionKey, provide, ref, Ref, computed, readonly, h } from "vue";

import TabNav from "./TabNav.vue";

export const V3TabsActiveTabName: InjectionKey<Ref<string | number>> = Symbol(
  "V3TabsActiveTabName"
);

export default {
  name: "v3-tabs",
  components: { TabNav },
  props: {
    activeTabName: [String, Number],
    contentStyle: [Object, String],
    defaultActiveTabName: [String, Number],
    tabPosition: {
      type: String,
      default: "top",
      validator<String>(val: string) {
        return ["top", "left", "bottom", "right"].includes(val);
      },
    },
    type: {
      type: String,
      default: "line",
      validator<String>(val: string) {
        return ["line", "card"].includes(val);
      },
    },
  },
  setup(props, context) {
    const getFirstTabName = (): string | number | undefined => {
      if (context.slots?.default) {
        const slots = context.slots.default();
        return slots[0]?.props?.name;
      }

      return undefined;
    };

    const current = ref(props.defaultActiveTabName || getFirstTabName());

    const currentTabName = computed(() => {
      if (props.activeTabName !== undefined) {
        return props.activeTabName;
      }

      return current.value;
    });

    provide(V3TabsActiveTabName, readonly(currentTabName));

    const activeTabLabel = ref<HTMLDivElement>(null);

    const activeTabLabelRect = computed(() => {
      if (activeTabLabel.value) {
        return activeTabLabel.value.getBoundingClientRect();
      }

      return null;
    });

    const onTab = (ev: MouseEvent, val: string, disabled: boolean | string) => {
      context.emit("click-tab", [ev, val]);

      if (!(disabled === true || disabled === "true")) {
        current.value = val;
        context.emit("update:active-tab-name", val);
      }
    };

    const renderLabels = () => {
      if (context.slots?.default) {
        return context.slots.default().map((vn) => {
          const label = (vn.children as any).label
            ? (vn.children as any).label()
            : vn.props.label;

          if (label === undefined) {
            throw new Error(
              `Each TabPane needs a label, which can be specified with "label" prop or named slot.`
            );
          }

          return h(
            "div",
            {
              class: `v3-tab-nav-label ${props.type}${
                currentTabName.value === vn.props.name ? " active" : ""
              }${
                vn.props.disabled === true || vn.props.disabled === "true"
                  ? " disabled"
                  : ""
              }`,
              style: vn.props.labelStyle || vn.props["label-style"],
              onClick: (ev: MouseEvent) =>
                onTab(ev, vn.props.name, vn.props.disabled),
              ref: (el: HTMLDivElement) => {
                if (currentTabName.value === vn.props.name) {
                  activeTabLabel.value = el;
                }
              },
            },
            label
          );
        });
      }

      return [];
    };

    return { activeTabLabelRect, renderLabels };
  },
};
</script>
<style lang="scss">
.v3-tabs {
  display: flex;
  width: 100%;
  background-color: #fff;

  &.top {
    flex-direction: column;

    > .v3-tabs-content {
      order: 2;
      padding-top: 8px;
    }
  }

  &.bottom {
    flex-direction: column;

    > .v3-tabs-content {
      order: 1;
      padding-bottom: 8px;
    }
  }

  &.left {
    > .v3-tabs-content {
      order: 2;
      padding-left: 16px;
    }
  }

  &.right {
    > .v3-tabs-content {
      order: 1;
      padding-right: 16px;
    }
  }

  > .v3-tabs-content {
    flex-grow: 1;
  }
}
</style>
