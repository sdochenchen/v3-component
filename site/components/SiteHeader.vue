<template>
  <div class="site-header">
    <v3-menu
      mode="horizontal"
      :style="{
        width: '100%',
        justifyContent: 'flex-end',
        borderColor: 'transparent',
      }"
      v-model:selected-key="selectedKey"
    >
      <v3-menu-item
        value="components"
        :style="{ width: '100px', textAlign: 'center' }"
        @click="onClick('components')"
      >
        组 件
      </v3-menu-item>
    </v3-menu>
  </div>
  <shadow-divider></shadow-divider>
</template>
<script lang="ts">
import { ref, onMounted, nextTick } from "vue";
import { useRouter, useRoute } from "vue-router";

import { Menu, MenuItem } from "../../components";
import ShadowDivider from "./ShadowDivider.vue";

export default {
  name: "site-header",
  components: {
    "v3-menu": Menu,
    "v3-menu-item": MenuItem,
    "shadow-divider": ShadowDivider,
  },
  setup(props, context) {
    const router = useRouter();

    const onClick = (key: string) => {
      router.push(`/${key}`);
    };

    const selectedKey = ref("components");

    onMounted(() => {
      setTimeout(() => {
        const first = router.currentRoute.value.path.indexOf("/");
        const last = router.currentRoute.value.path.lastIndexOf("/");
        const key = router.currentRoute.value.path.substr(
          first + 1,
          first === last ? undefined : last - first - 1
        );
        selectedKey.value = key;
      }, 0);
    });

    return { selectedKey, onClick };
  },
};
</script>
<style lang="scss" scoped>
.site-header {
  width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: flex-end;
  align-items: center;
}
</style>
