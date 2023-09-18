<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-item-group v-model="selected">
        <v-container>
          <v-row>
            <v-col cols="12" class="d-flex align-center">
              <span class="text-h6 pureple--text font-weight-black me-2">
                آرتیست‌های ما
              </span>
              <v-divider />
            </v-col>
            <v-col v-for="(a, i) in artists" :key="`artist-card-${i}`" cols="6">
              <v-item v-slot="{ active, toggle }" :value="i">
                <artist-card :artist="a" :active="active" @click="toggle" />
              </v-item>
            </v-col>
          </v-row>
        </v-container>
      </v-item-group>
      <v-container v-if="selectedArtist !== false">
        <v-row dense>
          <v-col cols="12" class="d-flex align-center">
            <div class="text-h6 pureple--text text--lighten-1 font-weight-black me-2">
              خدماتی که <span class="purple--text text--darken-2" v-text="selectedArtist.name" /> ارائه می‌دهد:
            </div>
          </v-col>
          <v-col cols="12" class="d-flex align-center">
            <span class="text--secondary">فیلتر‌ها: </span>
            <v-chip-group
              v-model="selectedCategory"
              active-class="pureple--text"
              row
            >
              <v-chip
                v-for="cat in categories"
                :key="cat.id"
                :value="cat.id"
              >
                {{ cat.title }}
              </v-chip>
            </v-chip-group>
          </v-col>
        </v-row>

        <transition-group v-if="servicesList.length > 0" name="list-complete" tag="div" class="row row--dense">
          <v-col v-for="(service, j) in servicesList" :key="`service-card-${j}`" cols="12" class="list-complete-item">
            <v-card class="default-card pureple--text text--darken-2">
              <div class="d-flex align-center pa-4">
                <span v-text="service.title" />
                <v-spacer />
                <span class="mt-1 font-weight-bold" v-text="nf(service.price, 1000)" />
                <div>
                  <v-img src="/icon-toman.svg" width="24" height="24" contain />
                </div>
              </div>
            </v-card>
          </v-col>
        </transition-group>
        <v-col v-else cols="12">
          <v-card class="default-card pureple--text text--darken-2">
            <v-card-text>
              <span>ای بابا! بنظر میاد که <span class="purple--text text--darken-2" v-text="selectedArtist.name" /> توی حوزه <span class="purple--text text--darken-2" v-text="selectedCategoryTitle" /> کاری انجام نمیده.</span>
            </v-card-text>
          </v-card>
        </v-col>
      </v-container>
    </v-col>
  </v-row>
</template>
<script>
import services from '~/schema/services'
export default {
  data () {
    return {
      selected: null,
      artists: [
        { id: 1, name: 'نسترن', img: 'avatar-1' },
        { id: 2, name: 'مونا', img: 'avatar-2' }
      ],
      categories: [
        { id: 1, title: 'اکستنشن مژه' },
        { id: 2, title: 'لیفت و لمینت' }
      ],
      selectedCategory: null
    }
  },
  computed: {
    selectedArtist () {
      if (this.selected !== null) {
        return this.artists[this.selected]
      } else {
        return false
      }
    },
    servicesList () {
      let list = services
      if (this.selectedArtist) {
        list = list.filter(s => s.artistID === this.selectedArtist.id)
      }
      if (this.selectedCategory) {
        list = list.filter(s => s.categoryID === this.selectedCategory)
      }
      return list
    },
    selectedCategoryTitle () {
      if (this.selectedCategory) {
        const cat = this.categories.find(c => c.id === this.selectedCategory)
        return cat.title
      } else {
        return ''
      }
    }
  },
  methods: {
    nf (value, multiplyBy = 1) {
      if (isNaN(value)) { return value }
      return Intl.NumberFormat('fa-IR').format(value * multiplyBy)
    }
  }
}
</script>
<style>
.list-complete-item {
  transition: all 1s;
  display: inline-block;
  margin-right: 0;
}
.list-complete-enter, .list-complete-leave-to
/* .list-complete-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateX(30px);
}
.list-complete-leave-active {
  position: relative;
}
</style>
