<template>
  <div class="container">
    <h4 class="title">按钮类型</h4>
    <div class="row">
      <v3-button :style="{ marginRight: '8px' }">
        Default
      </v3-button>
      <v3-button type="primary">
        Primary
      </v3-button>
    </div>
    <h4 class="title">危险按钮</h4>
    <div class="row">
      <v3-button :style="{ marginRight: '8px' }" :danger="true">
        Default
      </v3-button>
      <v3-button :style="{ marginRight: '8px' }" type="primary" :danger="true">
        Primary
      </v3-button>
    </div>
    <h4 class="title">图标按钮</h4>
    <div class="row">
      <v3-button :style="{ marginRight: '8px' }" icon-name="settings">
        Settings
      </v3-button>
      <v3-button type="primary" icon-name="airplane">
        Airplane
      </v3-button>
    </div>
    <h4 class="title">按钮大小</h4>
    <div class="row">
      <v3-button :style="{ marginRight: '8px' }" type="primary" size="small">
        Small
      </v3-button>
      <v3-button :style="{ marginRight: '8px' }" type="primary">
        Middle
      </v3-button>
      <v3-button size="large" type="primary">
        Large
      </v3-button>
    </div>
    <h4 class="title">禁用</h4>
    <div class="row">
      <v3-button :style="{ marginRight: '8px' }" disabled="true">
        Default
      </v3-button>
      <v3-button
        type="primary"
        :style="{ marginRight: '8px' }"
        :disabled="true"
      >
        Primary
      </v3-button>
      <v3-button
        :style="{ marginRight: '8px' }"
        :danger="true"
        disabled="true"
      >
        Danger
      </v3-button>
      <v3-button type="primary" :danger="true" :disabled="true">
        Danger
      </v3-button>
    </div>
    <h4 class="title">加载中</h4>
    <div class="row">
      <v3-button
        icon-name="cursor"
        type="primary"
        :loading="loading"
        @click="toggleLoading"
      >
        Click me!
      </v3-button>
    </div>
  </div>
</template>
<script lang="ts">
import { ref } from "vue";

import { Button } from "../../components";

export default {
  name: "button-example",
  components: { "v3-button": Button },
  setup() {
    const loading = ref(true);

    const toggleLoading = () => {
      loading.value = !loading.value;
    };

    return { loading, toggleLoading };
  },
};
</script>
<style lang="scss" scoped></style>
