<template>
  <v-row class="fill-height" style="height: 100vh;" justify="center" align="center">
    <v-col cols="12" sm="8" md="6" class="fill-height d-flex align-center justify-center flex-column">
      <v-img src="/beauty.png" contain class="mx-auto" style="flex:0 0 60%;" />
      <div class="text-center d-flex flex-column justify-space-around" style="flex: 0 0 30%;">
        <h1 class="text-center pureple--text text-h5 text-sm-h4 font-weight-black mb-3">
          تصمیم با تو!
        </h1>
        <h1 class="text-center pureple--text text-h6 text-sm-h5 font-weight-medium">
          آرایشگرت رو خودت انتخاب کن
        </h1>
        <v-btn
          large
          dark
          color="pureple"
          class="mt-2"
          rounded
          to="/choose-location"
        >
          <span class="font-weight-bolder text-h6 px-8">
            بزن بریم!
          </span>
        </v-btn>
      </div>
      <div class="spacer" style="flex: 1 0 10%;" />
    </v-col>
  </v-row>
</template>
