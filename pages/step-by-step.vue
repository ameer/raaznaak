<template>
  <div>
    <v-card>
      <v-card-title>
        <span class="text--primary font-weight-black" v-text="stepTitle" />
        <v-spacer />
        <v-progress-circular
          :rotate="0"
          :size="64"
          :width="4"
          :value="calculatedProgressValue"
          color="pureple lighten-1"
        >
          <span v-text="currentStep" />
          <span class="mx-1">از</span>
          <span v-text="totalStep" />
        </v-progress-circular>
      </v-card-title>
      <v-stepper v-model="stepModel">
        <v-stepper-items>
          <v-stepper-content class="pa-0" step="1">
            <services-categories />
          </v-stepper-content>
          <v-stepper-content class="pa-0" step="2">
            <services-location />
          </v-stepper-content>
          <v-stepper-content class="pa-0" step="3">
            <services-artists />
          </v-stepper-content>
        </v-stepper-items>
      </v-stepper>
    </v-card>
  </div>
</template>
<script>
export default {
  layout: 'v1',
  data () {
    return {
      stepModel: 1,
      stepsList: [
        {
          title: ''
        },
        {
          title: 'چه کاری از ما برمیاد؟'
        },
        {
          title: 'کجا برای شما راحت‌تره؟'
        },
        {
          title: 'با کدوم آرتیست؟'
        },
        {
          title: 'زمان دلخواه شما؟'
        }
      ]
    }
  },
  computed: {
    stepTitle () {
      return this.stepsList[this.stepModel].title
    },
    calculatedProgressValue () {
      return (this.stepModel - 1) * 34
    },
    currentStep () {
      return Intl.NumberFormat('fa-IR').format(this.stepModel)
    },
    totalStep () {
      return Intl.NumberFormat('fa-IR').format(this.stepsList.length - 1)
    }
  },
  created () {
    this.$nuxt.$on('nextStep', this.nextStep)
    this.$nuxt.$on('prevStep', this.prevStep)
  },
  beforeDestroy () {
    this.$nuxt.$off('nextStep', this.nextStep)
    this.$nuxt.$off('prevStep', this.prevStep)
  },
  methods: {
    nextStep () {
      if (this.stepModel < 4) {
        this.stepModel++
      }
    },
    prevStep () {
      if (this.stepModel > 1) {
        this.stepModel--
      }
    }
  }
}
</script>
<style>

</style>
