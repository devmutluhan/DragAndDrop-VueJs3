<template>
  <v-container>
    <v-spacer></v-spacer>
    <v-row>
      <v-col> SATIR YAPISINI SEÇINIZ </v-col>
      <v-col cols="auto">
        <v-icon
          @click="$emit('addClick', false)"
          icon="mdi-close"
          variant="text"
        ></v-icon>
      </v-col>
    </v-row>
    <v-row>
      <v-col v-for="item in sectionData" :key="item.id" cols="2">
        <v-card
          class="mx-auto elevation-0"
          variant="plain"
          @click="$emit('addClick', item)"
        >
          <svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 0 100 50">
            <path :d="[item.svgattr]" />
          </svg>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>
  
  <script>
export default {
  props: ["sectionData"],
  name: "RowStructure",
};
</script>
  
  <style>
</style>