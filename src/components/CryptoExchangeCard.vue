<template>
  <div>
    <q-card class="q-ma-md q-pa-sm">
      <q-card-section>
        <div class="text-h4">{{ ticker.market.name }}</div>
        <div class="text-h6">
          Trust: <q-avatar size="sm" :color="ticker.trust_score"></q-avatar>
        </div>
      </q-card-section>
      <q-separator></q-separator>
      <q-card-section>
        <div class="column flex flex-center">
          <div class="text-h4">
            <q-icon
              :name="changeInLast24Hr > 0 ? 'tending_up' : 'tending-down'"
              :color="changeInLast24Hr > 0 ? 'green' : 'red'"
              size="24px"
            />
            ${{ ticker.last }}
          </div>
          <div class="text-h5 q-pt-md">
            Volume:{{ ticker.volume.toFixed(2) }}
          </div>
        </div>
      </q-card-section>
      <q-card-actions class="flex flex-center">
        <q-btn
          type="a"
          color="primary"
          size="lg"
          :href="ticker.trade_url"
          target="__blank"
          flat
          >Trade</q-btn
        >
      </q-card-actions>
    </q-card>
  </div>
</template>

<script>
import { defineComponent, ref } from "vue";
export default defineComponent({
  name: "CryptoExchangeCard",
  props: {
    ticker: {
      type: Object,
      required: true,
    },
    changeInLast24Hr: {
      type: Number,
      required: true,
    },
  },
});
</script>

<style lang="scss" scoped></style>
