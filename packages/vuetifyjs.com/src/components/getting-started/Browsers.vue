<template>
  <v-list class="transparent py-0">
    <v-layout
      row
      wrap
    >
      <v-flex
        v-for="browser in browsers"
        :key="browser.title"
        px-0
        xs12
        sm6
        md4
      >
        <v-list-tile avatar>
          <v-list-tile-avatar
            :color="browser.supported ? browser.supported === 'polyfill' ? 'warning' : 'success' : 'error'"
          >
            <v-icon
              v-if="typeof browser.icon === 'string'"
              dark
            >fab fa-{{ browser.icon }}</v-icon>
            <v-icon
              v-for="icon in browser.icon"
              v-else
              :key="icon"
              class="browser-icon--split"
              dark
            >fab fa-{{ icon }}</v-icon>
          </v-list-tile-avatar>
          <v-list-tile-content>
            <v-list-tile-title>{{ browser.title }}</v-list-tile-title>
            <v-list-tile-sub-title><span>{{ $t(getBrowserSupport(browser)) }}</span></v-list-tile-sub-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-flex>
    </v-layout>
  </v-list>
</template>

<script>
  export default {
    data: () => ({
      browsers: [
        { icon: 'chrome', title: 'Chrome', supported: true },
        { icon: 'firefox', title: 'Firefox', supported: true },
        { icon: 'edge', title: 'Edge', supported: true },
        { icon: 'safari', title: 'Safari 10+', supported: true },
        { icon: ['internet-explorer', 'safari'], title: 'IE11 / Safari 9', supported: 'polyfill' },
        { icon: 'internet-explorer', title: 'IE9 / IE10', supported: false }
      ]
    }),

    methods: {
      getBrowserSupport (browser) {
        if (browser.supported === true) return 'GettingStarted.QuickStart.browserSupport.supported'
        else if (browser.supported === false) return 'GettingStarted.QuickStart.browserSupport.notSupported'
        else return `GettingStarted.QuickStart.browserSupport.${browser.supported}`
      }
    }
  }
</script>

<style lang="stylus">
  .browser-icon--split
    position: absolute

    &:nth-child(1)
      clip: rect(0px 21px 40px 0px)
    &:nth-child(2)
      clip: rect(0px 40px 40px 22px)
</style>
