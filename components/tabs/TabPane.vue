<template>
  <div class="v3-tab-pane" v-if="activeTabName === name">
    <slot></slot>
  </div>
</template>
<script lang="ts">
import { inject } from "vue";

import { V3TabsActiveTabName } from "./Tabs.vue";

export default {
  name: "v3-tab-pane",
  props: {
    disabled: { type: [Boolean, String], default: false },
    label: String,
    labelStyle: [Object, String],
    name: { type: [Number, String], required: true },
  },
  setup(props, context) {
    const activeTabName = inject(V3TabsActiveTabName);

    return { activeTabName };
  },
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-tab-pane {
  color: $v3-main;
  font-size: 14px;
}
</style>
