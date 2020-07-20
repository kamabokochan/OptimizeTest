<template>
  <div class="container">
    <div>
      <Logo v-if="isOptimizePage" />
      <h1 class="title">
        OptimizeTest
      </h1>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          rel="noopener noreferrer"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          rel="noopener noreferrer"
          class="button--grey"
        >
          GitHub
        </a>
        <nuxt-link to="/subPage">
          subPage
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Component } from 'nuxt-property-decorator'

declare global {
  interface Window {
      optimize: boolean,
      dataLayer: any
  }
}

@Component({})
export default class IndexPage extends Vue {
  isOptimizePage = false
  head () {
    return {
      script: [
        {
          innerHTML: "(function(a,s,y,n,c,h,i,d,e){s.className+=' '+y;h.start=1*new Date;h.end=i=function(){s.className=s.className.replace(RegExp(' ?'+y),'')};(a[n]=a[n]||[]).hide=h;setTimeout(function(){i();h.end=null},c);h.timeout=c;})(window,document.documentElement,'async-hide','dataLayer',4000,{'GTM-TLFTHCG':true});"
        },
        {
          src: 'https://www.googleoptimize.com/optimize.js?id=OPT-WRHD6Z3',
          onerror: 'dataLayer.hide.end && dataLayer.hide.end()'
        }
      ],
      __dangerouslyDisableSanitizers: ['script']
    }
  }

  mounted () {
    if (window.dataLayer) {
      window.dataLayer.push({ event: 'optimize.activate' })
    }
    if (window.optimize) {
      this.isOptimizePage = true
    }
  }
}
</script>

<style>
.async-hide { opacity: 0 !important}
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
