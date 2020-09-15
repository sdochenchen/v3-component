<template>
  <div class="container">
    <h4 class="title">基本使用</h4>
    <div class="row">
      <v3-input placeholder="Basic usage"> </v3-input>
    </div>
    <h4 class="title">三种大小</h4>
    <div class="row">
      <v3-input
        :label-attrs="{ style: { marginRight: '8px' } }"
        placeholder="Small..."
        size="small"
      >
      </v3-input>
      <v3-input
        :label-attrs="{ style: { marginRight: '8px' } }"
        placeholder="Middle..."
      >
      </v3-input>
      <v3-input placeholder="Large..." size="large"></v3-input>
    </div>
    <h4 class="title">三种状态</h4>
    <div class="row">
      <v3-input
        :label-attrs="{ style: { marginRight: '8px' } }"
        placeholder="Disabled..."
        :disabled="true"
      >
      </v3-input>
      <v3-input
        :label-attrs="{ style: { marginRight: '8px' } }"
        placeholder="Readonly..."
        :readonly="true"
      >
      </v3-input>
      <v3-input placeholder="Error..." :error="true"></v3-input>
    </div>
    <h4 class="title">前缀和后缀</h4>
    <div class="row">
      <v3-input
        :label-attrs="{ style: { marginRight: '8px' } }"
        prefixIconName="user"
      >
      </v3-input>
      <v3-input
        v-model:value="password1"
        :error="!!password1"
        prefix-icon-name="lock"
        suffix-icon-name="close"
        suffix-icon-style="cursor:pointer; width: 12px; height: 12px;"
        placeholder="Input..."
        @click-suffix="clear"
      >
      </v3-input>
    </div>
    <h4 class="title">密码框</h4>
    <div class="row">
      <v3-password v-model:value="password2"></v3-password>
    </div>
    <h4 class="title">文本框</h4>
    <div class="row">
      <v3-text-area :style="{ width: '250px', height: '100px' }">
      </v3-text-area>
    </div>
    <h4 class="title">原生类型</h4>
    <div class="row">
      <v3-input :label-attrs="{ style: { marginLeft: '8px' } }" type="number">
      </v3-input>
      <v3-input :label-attrs="{ style: { marginLeft: '8px' } }" type="range">
      </v3-input>
      <v3-input :label-attrs="{ style: { marginLeft: '8px' } }" type="radio">
      </v3-input>
      <v3-input :label-attrs="{ style: { width: '80px' } }" type="color">
      </v3-input>
    </div>
  </div>
</template>
<script lang="ts">
import { ref } from "vue";

import { Input, Password, TextArea } from "../../components";

export default {
  name: "input-example",
  components: {
    "v3-input": Input,
    "v3-password": Password,
    "v3-text-area": TextArea,
  },
  setup() {
    const password1 = ref("");
    const password2 = ref("");

    const clear = () => {
      password1.value = "";
    };

    return {
      password1,
      password2,
      clear,
    };
  },
};
</script>
<style lang="scss" scoped></style>
