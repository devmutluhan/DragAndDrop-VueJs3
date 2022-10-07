<template>
  <v-container>
    <v-col class="d-flex align-center flex-column pt-16">
      <v-icon
        @click="$emit('addClick', true)"
        icon="mdi-plus-circle"
        variant="text"
        size="8vh"
      ></v-icon>
      <v-col> Yeni Satır Ekle </v-col>
    </v-col>
  </v-container>
</template>

<script>
export default {
  name: "AddComponent",
};
</script>

<style>
</style>