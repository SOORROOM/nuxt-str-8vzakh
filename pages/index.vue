<template>
  <div>
    page index modif
    <v-card v-for="i in 7" width="400">
      <v-card-title>This is a title</v-card-title>
      <v-card-subtitle>This is a subtitle</v-card-subtitle>
      <v-card-text> This is content </v-card-text>
    </v-card>
    made with nuxt 3
    <v-btn variant="outlined" color="primary"
      >test <v-icon>mdi-pencil</v-icon></v-btn
    >
    <Account v-if="user" />
    <Auth v-else />
  </div>
</template>
<script setup>
const user = useSupabaseUser();
</script>
