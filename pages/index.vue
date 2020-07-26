<template>
  <div class="container">
    <div>
      <h1 v-if="variant === '0'">オリジナル</h1>
      <h1 v-if="variant === '1'">パターン1</h1>
      <h1 v-if="variant === '2'">パターン2</h1>
    </div>
    <div>
      <nuxt-link to="/subPage">
        subPage
      </nuxt-link>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import { Component } from 'nuxt-property-decorator'

declare global {
  interface Window {
      optimize: boolean,
      dataLayer: any,
      google_optimize: any
  }
}

@Component({})
export default class IndexPage extends Vue {
  variant: string = ''

  head () {
    return {
      script: [
        // {
        //   innerHTML: "(function(a,s,y,n,c,h,i,d,e){s.className+=' '+y;h.start=1*new Date;h.end=i=function(){s.className=s.className.replace(RegExp(' ?'+y),'')};(a[n]=a[n]||[]).hide=h;setTimeout(function(){i();h.end=null},c);h.timeout=c;})(window,document.documentElement,'async-hide','dataLayer',4000,{'GTM-TLFTHCG':true});"
        // },
        {
          src: 'https://www.googleoptimize.com/optimize.js?id=OPT-WRHD6Z3',
          onerror: 'dataLayer.hide.end && dataLayer.hide.end()'
        }
      ],
      __dangerouslyDisableSanitizers: ['script']
    }
  }

  async mounted () {
    if (window.dataLayer) {
      await window.dataLayer.push({ event: "optimize.activate" });
    }
    const intervalId = setInterval(() => {
      // googleootimizeが読み込まれるまでループ
      if (window.google_optimize !== undefined) {
        this.variant = window.google_optimize.get('wIOLBw_BTyaHPqjwWH8wWg');
        console.log(this.variant)
        clearInterval(intervalId);
      }
    }, 100);
  }
}
</script>

<style>
.async-hide { opacity: 0 !important}
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
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
