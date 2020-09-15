<template>
  <li class="v3-menu-group">
    <div class="v3-menu-group-title">
      <slot name="title"></slot>
    </div>
    <ul class="v3-menu-group-list">
      <slot></slot>
    </ul>
  </li>
</template>
<script lang="ts">
export default {
  name: "v3-menu-group",
};
</script>
<style lang="scss">
@import "../assets/var.scss";

.v3-menu-group {
  > .v3-menu-group-title {
    font-size: 12px;
    padding: 12px 24px 12px 36px;
    color: $v3-disable;
  }

  > .v3-menu-group-list {
    list-style: none;
    margin-bottom: 0;

    .v3-menu-item {
      padding: 12px 24px 12px 48px;
    }
  }
}
</style>
