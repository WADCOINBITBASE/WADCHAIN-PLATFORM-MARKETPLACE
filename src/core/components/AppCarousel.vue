<template>
  <div class="mew-component--banner-ads cursor--pointer">
    <mew6-white-sheet class="overflow--hidden">
      <v-carousel
        v-model="currentSlide"
        height="100%"
        hide-delimiters
        show-arrows-on-hover
        cycle
      >
        <v-carousel-item :ripple="false">
          <a
            rel="dofollow"
            :href="browserLink"
            target="_blank"
            @click="openEnkrypt"
          >
            <img
              class="slide-img"
              src="@/assets/images/slides/slide1.jpg"
              alt="Enkrypt"
            />
          </a>
        </v-carousel-item>
        <v-carousel-item :ripple="false">
          <a @click="openMewWallet">
            <img
              class="slide-img"
              src="@/assets/images/slides/slide2.jpg"
              alt="Enkrypt"
            />
          </a>
        </v-carousel-item>
        <v-carousel-item
          :ripple="false"
          :to="{ name: ROUTES_HOME.BUY_HARDWARE_WALLET.NAME }"
          target="_blank"
        >
          <img
            class="slide-img"
            src="@/assets/images/slides/slide3.jpg"
            alt="Enkrypt"
          />
        </v-carousel-item>
      </v-carousel>
    </mew6-white-sheet>
  </div>
</template>

<script>
import platform from 'platform';

import { ROUTES_HOME } from '@/core/configs/configRoutes';
import enkryptMarketing from '@/core/mixins/enkryptMarketing.mixin.js';
import handlerAnalytics from '@/modules/analytics-opt-in/handlers/handlerAnalytics.mixin.js';
export default {
  mixins: [enkryptMarketing, handlerAnalytics],
  data: () => ({
    currentSlide: 0,
    ROUTES_HOME: ROUTES_HOME
  }),
  computed: {
    mobileOrWebLink() {
      if (platform.os.family.includes('iOS')) {
        return 'https://apps.apple.com/app/id1464614025';
      } else if (platform.os.family.includes('Android')) {
        return 'https://play.google.com/store/apps/details?id=com.myetherwallet.mewwallet';
      }
      return 'https://www.mewwallet.com/';
    }
  },
  methods: {
    openMewWallet() {
      this.trackMewWalletInstall();
      // eslint-disable-next-line
      window.open(this.mobileOrWebLink, '_blank');
    },
    openEnkrypt() {
      this.trackEnkryptInstall();
    }
  }
};
</script>

<style lang="scss" scoped>
.slide-img {
  width: 100%;
  height: 100%;
}
</style>
