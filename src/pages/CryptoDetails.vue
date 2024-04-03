<template>
  <q-page padding>
    <div v-if="details">
      <CryptoDetailsHeader
        :image="details.image.small"
        :name="details.name"
        :symbol="details.symbol"
      ></CryptoDetailsHeader>

      <q-separator></q-separator>

      <CryptoDetailsSocialMediaButtons
        :facebookUserName="details.links.facebook_username"
        :twitterUserName="details.links.twitter_screen_name"
        :redditLink="details.links.subreddit_url"
      >
      </CryptoDetailsSocialMediaButtons>

      <div class="row q-pt-lg">
        <div class="col">
          <p v-html="details.description.en"></p>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h4>Exchange</h4>
        </div>
      </div>

      <div class="row">
        <div
          class="col-md-4 col-sm-6 col-xs-12"
          v-for="(ticker, index) in usdTickers"
          :key="index"
        >
          <crypto-exchange-card
            :ticker="ticker"
            :changeInLast24Hr="details.market_data.price_change_24h"
          ></crypto-exchange-card>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
import CryptoDetailsHeader from "src/components/CryptoDetailsHeader.vue";
import CryptoDetailsSocialMediaButtons from "src/components/CryptoDetailsSocialMediaButtons.vue";
import cryptoExchangeCard from "src/components/CryptoExchangeCard.vue";
import { defineComponent, ref } from "vue";

export default defineComponent({
  components: {
    CryptoDetailsHeader,
    CryptoDetailsSocialMediaButtons,
    cryptoExchangeCard,
  },
  data: () => ({
    details: undefined,
  }),
  async created() {
    try {
      const id = this.$route.params.id;

      if (!id) {
        alert("No ID specified! Please try again!");
        return;
      }

      const res = await this.$api.get(`coins/${id}`);

      res.status === 200
        ? (this.details = res.data)
        : alert("There was an error fetching the coin!");
    } catch (error) {
      alert("There was an error fetching the coin!");
    }
  },
  computed: {
    usdTickers() {
      return this.details.tickers.filter((ticker) => ticker.target === "USD");
    },
  },
});
</script>

<style lang="scss" scoped></style>
