<template>
  <div class="components-page">
    <div class="nav-bar">
      <v3-menu v-model:selected-key="selectedKey">
        <v3-menu-item value="overview" @click="onClick('overview')">
          组件总览
        </v3-menu-item>
        <v3-menu-group>
          <template v-slot:title>
            通用
          </template>
          <template v-slot:default>
            <v3-menu-item value="button" @click="onClick('button')">
              Button 按钮
            </v3-menu-item>
          </template>
        </v3-menu-group>
        <v3-menu-group>
          <template v-slot:title>
            导航
          </template>
          <template v-slot:default>
            <v3-menu-item value="menu" @click="onClick('menu')">
              Menu 导航菜单
            </v3-menu-item>
          </template>
        </v3-menu-group>
        <v3-menu-group>
          <template v-slot:title>
            数据录入
          </template>
          <template v-slot:default>
            <v3-menu-item value="input" @click="onClick('input')">
              Input 输入框
            </v3-menu-item>
            <v3-menu-item value="select" @click="onClick('select')">
              Selelct 选择器
            </v3-menu-item>
            <v3-menu-item value="switch" @click="onClick('switch')">
              Switch 开关
            </v3-menu-item>
          </template>
        </v3-menu-group>
        <v3-menu-group>
          <template v-slot:title>
            数据展示
          </template>
          <template v-slot:default>
            <v3-menu-item value="tabs" @click="onClick('tabs')">
              Tabs 标签页
            </v3-menu-item>
          </template>
        </v3-menu-group>
      </v3-menu>
    </div>
    <div class="example-container">
      <router-view></router-view>
    </div>
  </div>
</template>
<script lang="ts">
import { ref, onMounted } from "vue";
import { useRouter } from "vue-router";

import { Menu, MenuGroup, MenuItem } from "../../components";

export default {
  name: "components-page",
  components: {
    "v3-menu": Menu,
    "v3-menu-group": MenuGroup,
    "v3-menu-item": MenuItem,
  },
  props: {},
  setup(props, context) {
    const router = useRouter();

    const path = router.currentRoute.value.path;
    const index = path.lastIndexOf("/");

    const onClick = (key: string) => {
      router.push(`/components/${key}`);
    };

    const selectedKey = ref("overview");

    onMounted(() => {
      setTimeout(() => {
        const index = router.currentRoute.value.path.lastIndexOf("/");
        const key = router.currentRoute.value.path.substr(index + 1);
        selectedKey.value = key;
      }, 0);
    });

    return { selectedKey, onClick };
  },
};
</script>
<style lang="scss">
.components-page {
  width: 1000px;
  margin: 0 auto;
  display: flex;

  .nav-bar {
    width: 240px;
    flex-shrink: 0;
  }

  .example-container {
    flex-grow: 1;
    padding: 0 40px;

    .container {
      width: 100%;
      margin: 20px 0;

      .title {
        color: #262626;
        margin-bottom: 16px;
      }

      .row {
        margin-bottom: 16px;
        display: flex;
        justify-content: flex-start;
        align-items: center;
      }
    }
  }
}
</style>
