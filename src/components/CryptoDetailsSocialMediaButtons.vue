<template>
  <div class="row q-pt-lg">
    <div class="col flex flex-center">
      <q-btn
        v-if="facebookUserName"
        type="a"
        color="primary"
        class="q-mr-md q-px-xl"
        :href="`https://facebook.com/${facebookUserName}`"
        target="__blank"
      >
        <q-icon class="q-pr-sm" name="mdi-facebook">Facebook</q-icon>
      </q-btn>

      <q-btn
        v-if="twitterUserName"
        type="a"
        color="blue"
        class="q-mr-md q-px-xl"
        :href="`https://twitter.com/${twitterUserName}`"
        target="__blank"
      >
        <q-icon class="q-pr-sm" name="mdi-twitter">Twitter</q-icon>
      </q-btn>

      <q-btn
        v-if="redditLink"
        type="a"
        color="black"
        class="q-mr-md q-px-xl"
        :href="redditLink"
        target="__blank"
      >
        <q-icon class="q-pr-sm" name="mdi-reddit">Reddit</q-icon>
      </q-btn>
    </div>
  </div>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "CryptoDetailsSocialMediaButtons",
  props: {
    facebookUserName: {
      type: String,
      required: true,
    },
    twitterUserName: {
      type: String,
      required: true,
    },
    redditLink: {
      type: String,
      required: true,
    },
  },
});
</script>

<style lang="scss" scoped></style>
