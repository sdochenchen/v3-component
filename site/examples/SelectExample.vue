<template>
  <div class="container">
    <h4 class="title">基本使用</h4>
    <div class="row">
      <v3-select defaultValue="lucy">
        <v3-option value="lucy" label="Lucy"></v3-option>
        <v3-option value="jack" label="Jack"></v3-option>
        <v3-option value="disabled" label="Disabled" :disabled="true">
        </v3-option>
        <v3-option value="lily" label="Lily"></v3-option>
      </v3-select>
    </div>
    <h4 class="title">三种大小</h4>
    <div class="row">
      <v3-select defaultValue="lucy" size="small" style="margin-right: 8px;">
        <v3-option value="lucy" label="Lucy"></v3-option>
        <v3-option value="jack" label="Jack"></v3-option>
        <v3-option value="disabled" label="Disabled" :disabled="true">
        </v3-option>
        <v3-option value="lily" label="Lily"></v3-option>
      </v3-select>
      <v3-select
        defaultValue="lucy"
        style="margin-right: 8px;"
        allow-clear="true"
      >
        <v3-option value="lucy" label="Lucy"></v3-option>
        <v3-option value="jack" label="Jack"></v3-option>
        <v3-option value="disabled" label="Disabled" :disabled="true">
        </v3-option>
        <v3-option value="lily" label="Lily"></v3-option>
      </v3-select>
      <v3-select defaultValue="lucy" size="large">
        <v3-option value="lucy" label="Lucy"></v3-option>
        <v3-option value="jack" label="Jack"></v3-option>
        <v3-option value="disabled" label="Disabled" :disabled="true">
        </v3-option>
        <v3-option value="lily" label="Lily"></v3-option>
      </v3-select>
    </div>
  </div>
</template>
<script lang="ts">
import { ref } from "vue";

import { Select, Option } from "../../components";

export default {
  name: "select-example",
  components: { "v3-select": Select, "v3-option": Option },
};
</script>
<style lang="scss" scoped></style>
