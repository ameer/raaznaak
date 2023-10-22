<template>
  <v-item-group>
    <v-container>
      <v-row>
        <v-col v-for="(a, i) in artists" :key="`ac-${i}`" cols="6">
          <v-item v-slot="{ active, toggle }">
            <artist-card :artist="a" :active="active" @click="toggle" />
          </v-item>
        </v-col>
      </v-row>
    </v-container>
  </v-item-group>
</template>
<script>
export default {
  data () {
    return {
      artists: [
        {
          text: 'مونا',
          value: 1,
          img: 'avatar-1'
        },
        {
          text: 'نسترن',
          value: 2,
          img: 'avatar-2'
        },
        {
          text: 'صبا',
          value: 3,
          img: 'avatar-3'
        },
        {
          text: 'مریم',
          value: 4,
          img: 'avatar-4'
        }
      ]
    }
  }
}
</script>
<style>
</style>
