<template>
  <div class="container">
    <h4 class="title">两种样式</h4>
    <div class="row" :style="{ height: '150px' }">
      <v3-tabs default-active-tab-name="tab-1" type="line">
        <v3-tab-pane name="tab-1">
          <template v-slot:label>
            <span>Tab-One</span>
          </template>
          <template v-slot:default>
            <div>Content of Tab Pane 1</div>
            <div>Content of Tab Pane 1</div>
            <div>Content of Tab Pane 1</div>
          </template>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Two" name="tab-2">
          <div>Content of Tab Pane 2</div>
          <div>Content of Tab Pane 2</div>
          <div>Content of Tab Pane 2</div>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Three" name="tab-3">
          <div>Content of Tab Pane 3</div>
          <div>Content of Tab Pane 3</div>
          <div>Content of Tab Pane 3</div>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Four" name="tab-4" :disabled="true">
          <div>Content of Tab Pane 4</div>
          <div>Content of Tab Pane 4</div>
          <div>Content of Tab Pane 4</div>
        </v3-tab-pane>
      </v3-tabs>
    </div>
    <div class="row" :style="{ height: '150px' }">
      <v3-tabs default-active-tab-name="tab-2" type="card">
        <v3-tab-pane name="tab-1">
          <template v-slot:label>
            <span>Tab-One</span>
          </template>
          <template v-slot:default>
            <div>Content of Tab Pane 1</div>
            <div>Content of Tab Pane 1</div>
            <div>Content of Tab Pane 1</div>
          </template>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Two" name="tab-2">
          <div>Content of Tab Pane 2</div>
          <div>Content of Tab Pane 2</div>
          <div>Content of Tab Pane 2</div>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Three" name="tab-3">
          <div>Content of Tab Pane 3</div>
          <div>Content of Tab Pane 3</div>
          <div>Content of Tab Pane 3</div>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Four" name="tab-4" :disabled="true">
          <div>Content of Tab Pane 4</div>
          <div>Content of Tab Pane 4</div>
          <div>Content of Tab Pane 4</div>
        </v3-tab-pane>
      </v3-tabs>
    </div>
    <h4 class="title">四种位置</h4>
    <div class="row">
      <v3-select
        v-model:value="position"
        allow-clear="false"
        style="width: 100px;"
      >
        <v3-option value="top" label="Top"></v3-option>
        <v3-option value="left" label="Left"></v3-option>
        <v3-option value="right" label="Right"></v3-option>
        <v3-option value="bottom" label="Bottom"></v3-option>
      </v3-select>
    </div>
    <div class="row" :style="{ height: '150px' }">
      <v3-tabs
        default-active-tab-name="tab-1"
        type="line"
        :tab-position="position"
        :key="position"
      >
        <v3-tab-pane name="tab-1">
          <template v-slot:label>
            <span>Tab-One</span>
          </template>
          <template v-slot:default>
            <div>Content of Tab Pane 1</div>
            <div>Content of Tab Pane 1</div>
            <div>Content of Tab Pane 1</div>
          </template>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Two" name="tab-2">
          <div>Content of Tab Pane 2</div>
          <div>Content of Tab Pane 2</div>
          <div>Content of Tab Pane 2</div>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Three" name="tab-3">
          <div>Content of Tab Pane 3</div>
          <div>Content of Tab Pane 3</div>
          <div>Content of Tab Pane 3</div>
        </v3-tab-pane>
        <v3-tab-pane label="Tab-Four" name="tab-4" :disabled="true">
          <div>Content of Tab Pane 4</div>
          <div>Content of Tab Pane 4</div>
          <div>Content of Tab Pane 4</div>
        </v3-tab-pane>
      </v3-tabs>
    </div>
  </div>
</template>
<script lang="ts">
import { ref } from "vue";

import { Button, Select, Option, Tabs, TabPane } from "../../components";

export default {
  name: "tabs-example",
  components: {
    "v3-button": Button,
    "v3-select": Select,
    "v3-option": Option,
    "v3-tabs": Tabs,
    "v3-tab-pane": TabPane,
  },
  setup() {
    const position = ref("top");
    const setPosition = (val: string) => {
      position.value = val;
    };

    return {
      position,
      setPosition,
    };
  },
};
</script>
<style lang="scss" scoped></style>
