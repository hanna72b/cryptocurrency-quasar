<template>
  <q-page>
    <div class="q-pa-md">
      <q-table
        grid
        flat
        bordered
        card-class="bg-primary text-white"
        :rows="coins"
        :columns="columns"
        row-key="name"
        :filter="filter"
        hide-header
        :pagination="{ rowsPerPage: 12 }"
        :rows-per-page-options="[12, 24, 48, 96]"
      >
        <template v-slot:top-right>
          <q-input
            borderless
            dense
            debounce="300"
            v-model="filter"
            placeholder="Search"
          >
            <template v-slot:append>
              <q-icon name="search" />
            </template>
          </q-input>
        </template>

        <template v-slot:item="props">
          <div class="q-pa-xs col-xs-12 col-sm-6 col-md-4">
            <q-card>
              <q-card-section class="text-center">
                <span class="text-h6">
                  {{ props.row.name }}
                </span>
              </q-card-section>
              <q-separator></q-separator>
              <q-card-section
                class="flex flex-center text-center"
                style="font-size: 34px"
              >
                {{ props.row.symbol }}
              </q-card-section>
              <q-card-actions class="flex flex-center">
                <q-btn
                  size="lg"
                  color="primary"
                  label="View"
                  @click="navToCryptoDetails(props.row.id)"
                ></q-btn>
              </q-card-actions>
            </q-card>
          </div>
        </template>
      </q-table>
    </div>
  </q-page>
</template>

<script>
import { defineComponent, ref } from "vue";

export default defineComponent({
  name: "IndexPage",
  data: () => ({
    coins: [],
    columns: [
      { name: "name", align: "center", label: "Name", field: "name" },
      { name: "symbol", align: "center", label: "Symbol", field: "symbol" },
    ],
    filter: "",
  }),
  async created() {
    try {
      const res = await this.$api.get("coins/list");
      res.status === 200
        ? (this.coins = res.data)
        : alert("There was an error fetching the coins");
    } catch (error) {
      alert("There was an error fetching the coins");
    }
  },
  methods: {
    navToCryptoDetails(id) {
      this.$router.push({ name: "CryptoDetails", params: { id } });
    },
  },
});
</script>
