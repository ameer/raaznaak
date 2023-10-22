<template>
  <v-item-group>
    <v-container>
      <v-row>
        <v-col v-for="(cat, i) in categories" :key="`cc-${i}`" cols="6">
          <v-item v-slot="{ active, toggle }">
            <v-btn
              block
              :outlined="!active"
              :dark="active"
              color="pureple"
              @click="toggle"
            >
              <span v-text="cat.text" />
            </v-btn>
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
      categories: [
        {
          text: 'اکستنشن مژه',
          value: 1
        },
        {
          text: 'لیفت و لمینت',
          value: 2
        },
        {
          text: 'رنگ مو',
          value: 3
        },
        {
          text: 'اصلاح صورت وابرو',
          value: 4
        },
        {
          text: 'کاشت هیدن',
          value: 5
        },
        {
          text: 'فیشیال پوست',
          value: 6
        },
        {
          text: 'لاک و ژلیش',
          value: 7
        },
        {
          text: 'مانیکور',
          value: 8
        },
        {
          text: 'بافت مو',
          value: 9
        }
      ]
    }
  }
}
</script>
<style>
</style>
