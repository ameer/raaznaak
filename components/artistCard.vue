<template>
  <v-card class="default-card rounded-xl" color="#f5f5f5" :ripple="false" @click="$emit('click')">
    <div class="text-center">
      <v-avatar size="64">
        <v-img :src="`/${imgSrc}.png`" />
      </v-avatar>
    </div>
    <v-card-title class="justify-center pt-2">
      {{ artist.name }}
    </v-card-title>
    <v-card-subtitle class="text-center">
      <v-rating
        empty-icon="mdi-star-outline"
        full-icon="mdi-star"
        half-icon="mdi-star-half-full"
        length="5"
        color="amber darken-1"
        readonly
        size="16"
        :value="5"
      />
    </v-card-subtitle>
    <v-card-actions>
      <v-btn :outlined="!active" block rounded color="pureple" dark>
        <v-icon v-if="active">
          mdi-check
        </v-icon>
        <span v-else>انتخاب</span>
      </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  props: {
    active: {
      type: Boolean,
      default: false
    },
    artist: {
      type: Object,
      default: () => ({
        name: 'نسترن',
        img: 'avatar'
      })
    }
  },
  computed: {
    imgSrc () {
      return this.active ? `${this.artist.img}--happy` : this.artist.img
    }
  }
}
</script>
<style>

</style>
