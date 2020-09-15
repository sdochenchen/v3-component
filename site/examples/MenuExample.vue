<template>
  <div class="container">
    <h4 class="title">横向菜单</h4>
    <div class="row">
      <v3-menu
        mode="horizontal"
        default-selected-key="option-1"
        @select="onSelect"
        @open-change="onOpenChange"
      >
        <v3-menu-item value="option-1" style="width: 220px;">
          <div class="sub-title">
            <v3-icon name="settings" style="margin-right: 8px;"></v3-icon>
            Navigation One
          </div>
        </v3-menu-item>
        <v3-sub-menu value="navigation-2" style="width: 220px;">
          <template v-slot:title>
            <div class="sub-title">
              <v3-icon name="thumbnails" style="margin-right: 8px;">
              </v3-icon>
              Navigation Two
            </div>
          </template>
          <template v-slot:default>
            <v3-menu-item value="option-2">Option 2</v3-menu-item>
            <v3-menu-item value="option-3">Option 3</v3-menu-item>
            <v3-sub-menu value="sub-menu">
              <template v-slot:title>
                <div class="sub-title">
                  <v3-icon name="database" style="margin-right: 8px;">
                  </v3-icon>
                  Sub Menu
                </div>
              </template>
              <template v-slot:default>
                <v3-menu-item value="option-4">Option 4</v3-menu-item>
                <v3-menu-item value="option-5">Option 5</v3-menu-item>
              </template>
            </v3-sub-menu>
          </template>
        </v3-sub-menu>
        <v3-sub-menu value="navigation-3" style="width: 220px;">
          <template v-slot:title>
            <div class="sub-title">
              <v3-icon name="graph-bar" style="margin-right: 8px;"></v3-icon>
              Navigation Three
            </div>
          </template>
          <template v-slot:default>
            <v3-menu-item value="option-6">Option 6</v3-menu-item>
            <v3-menu-item value="option-7">Option 7</v3-menu-item>
          </template>
        </v3-sub-menu>
        <v3-sub-menu
          value="navigation-4"
          style="width: 220px;"
          disabled="true"
        >
          <template v-slot:title>
            <div class="sub-title">
              <v3-icon name="records" style="margin-right: 8px;"></v3-icon>
              Navigation Four
            </div>
          </template>
          <template v-slot:default>
            <v3-menu-item value="option-8">Option 8</v3-menu-item>
            <v3-menu-item value="option-9">Option 9</v3-menu-item>
          </template>
        </v3-sub-menu>
      </v3-menu>
    </div>
    <h4 class="title">纵向菜单</h4>
    <div class="row">
      <v3-menu
        style="width: 220px;"
        default-selected-key="option-1"
        :default-open-keys="['navigation-1', 'navigation-2']"
      >
        <v3-menu-item value="option-1">Option 1</v3-menu-item>
        <v3-menu-item value="option-2" :disabled="true">
          Option 2
        </v3-menu-item>
        <v3-sub-menu value="navigation-1" :show-arrow="false">
          <template v-slot:title>
            <div class="sub-title">
              <v3-icon name="settings" style="margin-right: 8px;"></v3-icon>
              Navigation One
            </div>
          </template>
          <template v-slot:default>
            <v3-menu-item value="option-3">Option 3</v3-menu-item>
            <v3-menu-item value="option-4">Option 4</v3-menu-item>
          </template>
        </v3-sub-menu>
        <v3-menu-item value="option-5">Option 5</v3-menu-item>
        <v3-sub-menu value="navigation-2">
          <template v-slot:title>
            <div class="sub-title">
              <v3-icon name="thumbnails" style="margin-right: 8px;">
              </v3-icon>
              Navigation Two
            </div>
          </template>
          <template v-slot:default>
            <v3-menu-group>
              <template v-slot:title>
                Group One
              </template>
              <template v-slot:default>
                <v3-menu-item value="option-6">Option 6</v3-menu-item>
                <v3-menu-item value="option-7">Option 7</v3-menu-item>
              </template>
            </v3-menu-group>
            <v3-menu-group>
              <template v-slot:title>
                Group Two
              </template>
              <template v-slot:default>
                <v3-menu-item value="option-8" :disabled="true"
                  >Option 8</v3-menu-item
                >
                <v3-menu-item value="option-9">Option 9</v3-menu-item>
              </template>
            </v3-menu-group>
          </template>
        </v3-sub-menu>
        <v3-menu-item value="option-10">Option 10</v3-menu-item>
      </v3-menu>
    </div>
  </div>
</template>
<script lang="ts">
import { Icon } from "v3-icons";

import { Menu, MenuGroup, MenuItem, SubMenu } from "../../components";

export default {
  name: "button-example",
  components: {
    "v3-icon": Icon,
    "v3-menu": Menu,
    "v3-menu-group": MenuGroup,
    "v3-menu-item": MenuItem,
    "v3-sub-menu": SubMenu,
  },
  setup() {
    const onSelect = (key: string | number) => {
      console.log(key);
    };

    const onOpenChange = (keys: Array<string | number>) => {
      console.log(keys);
    };

    return { onSelect, onOpenChange };
  },
};
</script>
<style lang="scss" scoped>
.sub-title {
  display: flex;
  justify-content: flex-start;
  align-items: center;
}
</style>
