<template>
  <div>
    Plaid Link is &nbsp;<b v-if="!plaidLoaded">NOT&nbsp;</b> loaded.
  </div>
</template>

<script>
import Vue from 'vue'
import LoadScript from 'vue-plugin-load-script'
Vue.use(LoadScript)

export default {
  data () {
    return {
      plaidLoaded: false,
      linkHandler: {}
    }
  },
  created () {
    Vue.loadScript('https://cdn.plaid.com/link/v2/stable/link-initialize.js')
      .then(() => {
        this.linkHandler = window.Plaid.create({
          forceIframe: true,
          env: 'sandbox',
          apiVersion: 'v2',
          clientName: 'Client Name',
          product: ['transactions'],
          key: process.env.PLAID_PUBLIC_KEY,
          onSuccess: () => {},
          onExit: () => {},
          onLoad: () => { this.plaidLoaded = true }
        })
      })
  },
  methods: {

  }
}
</script>

<style lang="stylus">
div
  display flex
  width 100vw
  height 100vh
  justify-content center
  align-items center
</style>
