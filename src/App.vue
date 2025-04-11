<template>
  <v-app>
    <v-app-bar app color="secondary" dark>
      <v-toolbar-title @click="goHome" class="cursor-pointer">
        Contact Saver
      </v-toolbar-title>
    </v-app-bar>

    <v-main>
      <v-container class="py-4">
        <router-view />
      </v-container>
    </v-main>

    <v-footer app padless color="secondary">
      <v-col class="text-center" style="font-size: 20px;" cols="12">
        © {{ new Date().getFullYear() }} Contact Saver
      </v-col>
    </v-footer>
  </v-app>
</template>

<script setup>
import { useRouter } from 'vue-router';

const router = useRouter();

const goHome = () => {
  router.push('/');
};
</script>

<style scoped>
.v-toolbar-title {
  font-weight: bold;
}

.cursor-pointer {
  cursor: pointer;
}
</style>
