<template>
  <v-row justify="center">
    <v-col cols="12" sm="8" md="6">
      <v-container>
        <v-row align="stretch">
          <v-col cols="12" class="d-flex align-center">
            <span class="text-h6 pureple--text font-weight-black me-2">
              انتخاب نزدیک‌ترین سالن
            </span>
            <v-divider />
            <v-btn rounded dark class="purple darken-3 mr-2" to="/booking">
              <span>بزن بریم!</span>
              <v-icon right>
                mdi-arrow-left
              </v-icon>
            </v-btn>
          </v-col>
          <v-col cols="12" md="6">
            <v-list
              subheader
              two-line
              rounded
              class="fill-height"
            >
              <v-list-item-group v-model="selectedPlaceIndex" class="pt-2">
                <v-list-item
                  v-for="(place, i) in placesInfo"
                  :key="`place-${i}`"
                >
                  <v-list-item-avatar size="20">
                    <v-scroll-y-reverse-transition>
                      <v-icon
                        v-if="selectedPlaceIndex === i"
                        class="green lighten-1"
                        color="white"
                        size="16"
                      >
                        mdi-check
                      </v-icon>
                    </v-scroll-y-reverse-transition>
                  </v-list-item-avatar>

                  <v-list-item-content>
                    <v-list-item-title class="font-weight-bold" v-text="place.title" />

                    <v-list-item-subtitle v-text="place.address" />
                  </v-list-item-content>

                  <v-list-item-action>
                    <v-btn
                      dark
                      icon
                      color="green"
                      class="elevation-0"
                      :href="'tel:'+place.phone"
                    >
                      <v-icon>mdi-phone</v-icon>
                    </v-btn>
                  </v-list-item-action>
                </v-list-item>
              </v-list-item-group>
            </v-list>
          </v-col>
          <v-col cols="12" md="6">
            <v-card class="pureple--text text--darken-2" style="position: relative;">
              <v-overlay :value="loadingMap" absolute opacity="1">
                <div class="d-flex flex-column align-center">
                  <v-progress-circular
                    indeterminate
                    size="64"
                  />
                  <div class="mt-2">
                    در حال بارگذاری نقشه
                  </div>
                </div>
              </v-overlay>
              <mapir :center="center" :api-key="apiKey" style="min-height: 400px;" @load="onMapLoaded">
                <mapMarker
                  v-for="(p, i) in places"
                  :key="i"
                  :coordinates="p"
                  :color="selectedPlaceIndex === i ? 'blue' : 'red'"
                  :draggable="false"
                  @click="markerOnClick(i)"
                />
              </mapir>
              <!-- <template v-if="selectedPlace">
                <v-card-title>
                  {{ selectedPlace.title }}
                </v-card-title>
                <v-card-text>
                  {{ selectedPlace.address }}
                </v-card-text>
                <v-card-actions>
                  <v-spacer />
                  <v-btn
                    small
                    dark
                    fab
                    color="green"
                    class="elevation-0"
                    :href="'tel:'+selectedPlace.phone"
                  >
                    <v-icon>mdi-phone</v-icon>
                  </v-btn>
                </v-card-actions>
              </template> -->
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-col>
  </v-row>
</template>
<script>
import { mapir, mapMarker } from 'mapir-vue'

export default {
  components: { mapir, mapMarker },
  data () {
    return {
      apiKey: 'eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsImp0aSI6IjUxZmExMTI0OGYzMDFlOThjNDA4ZTliY2JjODdlNjk5NTkyODMyMTQzN2QzNTIxZjM5NmM0MjFjMWJmODUzY2FmNDQ5ZDExOTJhNTU1ZDgwIn0.eyJhdWQiOiIzODczIiwianRpIjoiNTFmYTExMjQ4ZjMwMWU5OGM0MDhlOWJjYmM4N2U2OTk1OTI4MzIxNDM3ZDM1MjFmMzk2YzQyMWMxYmY4NTNjYWY0NDlkMTE5MmE1NTVkODAiLCJpYXQiOjE1NjQ1NjA0ODEsIm5iZiI6MTU2NDU2MDQ4MSwiZXhwIjoxNTY3MjM4ODgwLCJzdWIiOiIiLCJzY29wZXMiOlsiYmFzaWMiXX0.cJ0wnLLCCSlTNDVtTYgYgUujQ1YSn9aNGURjurlSX3kajoq_620Xcrvl-wQZcMyCxdVGtG2Z65Ic3rd7ccodP1aCPFUU0ajRN24dSFvXXJ-nFtvk4fXw6WBSaJ3368j4oob9EddRb_X95uMiZRTgPa3ScLu8fHAgLn27wqpbiNL5KPMGTWgAgA64h6dPIuVIvH7L6tetHOnKzFnBgLV0tokXwRt7yPW6fk7Y6-GbLnQGce7kziNsC2EYYTNaXtSpuVAvojcQNz95zbjlVuGYFAn9S_O24YvE2o8cbhVQQ2fiUYL6FSmmR-E-SiT9ubmDwpjfCLrka-nIFP9qE6KpAg',
      center: [51.420296, 35.732379],
      markerCoordinates: [51.420296, 35.732379],
      loadingMap: true,
      places: [
        [51.420296, 35.732379],
        [51.391876, 35.700924],
        [51.455262, 35.742524],
        [51.471934, 35.797592]
      ],
      placesInfo: [
        { title: 'عروس سرای نیلوفر', address: 'آدرس: تهران، محله ساعی، بزرگراه آیت الله مدرس', phone: '021987654321' },
        { title: 'نارسیس بیوتی', address: 'تهران، محله فاطمی، مرتضی مظفری خواه، رهی معیری، آونگ', phone: '02169857536' },
        { title: 'عروس شرقی', address: 'تهران، محله جمالزاده (حشمت الدوله-جمالزاده)، جمالزاده، کاج، سپیدار', phone: '02112345678' },
        { title: 'سالن خدمات زیبایی عروس برتر', address: 'تهران، محله دیباجی - فرمانیه (فرمانيه)، شعله، کوهستان هشتم، لادن', phone: '02112345678' }
      ],
      selectedPlaceIndex: null
    }
  },
  computed: {
    selectedPlace () {
      if (this.selectedPlaceIndex !== null) { return this.placesInfo[this.selectedPlaceIndex] }
      return false
    }
  },
  methods: {
    onMapLoaded () {
      this.loadingMap = false
    },
    markerOnClick (index) {
      this.selectedPlaceIndex = index
    }
  }
}
</script>
<style></style>
