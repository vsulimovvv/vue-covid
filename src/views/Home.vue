<template>
  <main v-if="!loading" class="pb-5">
    <DataTitle :text="title" :dataDate="dataDate" />
    <CountrySelect @get-country="getCountryData" :countries="countries" />
    <DataBoxes :stats="stats" />

    <button
      @click="clearCountryData"
      v-if="stats.Country"
      class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600 active:scale-[0.98]"
    >
      Очистить
    </button>
  </main>

  <main v-else class="flex flex-col align-center justify-center text-center">
    <div class="text-gray-500 text-3xl mt-10 mb-6">Загрузка данных</div>

    <img :src="loadingImage" class="w-24 m-auto" alt="loading" />
  </main>
</template>

<script>
import DataTitle from '@/components/DataTitle';
import DataBoxes from '@/components/DataBoxes';
import CountrySelect from '@/components/CountrySelect';

export default {
  name: 'Home',
  components: { DataTitle, DataBoxes, CountrySelect },

  data() {
    return {
      loading: true,
      title: 'Мир',
      dataDate: '',
      stats: {},
      countries: [],
      loadingImage: require('../assets/hourglass.gif'),
    };
  },

  async created() {
    const data = await this.fetchCovidData();

    this.dataDate = data.Date;
    this.stats = data.Global;
    this.countries = data.Countries;
    this.loading = false;
  },

  methods: {
    async fetchCovidData() {
      const res = await fetch('https://api.covid19api.com/summary');
      const data = await res.json();
      return data;
    },

    getCountryData(country) {
      this.stats = country;
      this.title = country.Country;
    },

    async clearCountryData() {
      this.loading = true;
      const data = await this.fetchCovidData();
      this.stats = data.Global;
      this.title = 'Мир';
      this.loading = false;
    },
  },
};
</script>
