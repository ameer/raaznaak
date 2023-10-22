<template>
  <v-app dark>
    <v-main>
      <Nuxt />
    </v-main>
    <v-footer app fixed>
      <v-container class="d-flex align-center justify-space-between">
        <v-btn color="pureple" dark @click="$nuxt.$emit('nextStep')">
          مرحله بعد
        </v-btn>
        <v-btn color="pureple" outlined @click="$nuxt.$emit('prevStep')">
          مرحله قبل
        </v-btn>
      </v-container>
    </v-footer>
  </v-app>
</template>

<script>
export default {
}
</script>
