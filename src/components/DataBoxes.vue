<template>
  <!-- Box 1 -->
  <div class="grid md:grid-cols-2 gap-4">
    <!-- Box 1 -->
    <div class="shadow-md bg-green-100 p-10 text-center rounded">
      <h3 class="text-2xl text-green-900 font-bold mb-4 md:text-3xl">
        Заражений
      </h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">Новые:</span>
        {{ numberWithCommas(stats.NewConfirmed) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Всего:</span>
        {{ numberWithCommas(stats.TotalConfirmed) }}
      </div>
    </div>
    <!-- Box 2 -->
    <div class="shadow-md bg-green-200 p-10 text-center rounded">
      <h3 class="text-2xl text-green-900 font-bold mb-4 md:text-3xl">
        Смертей
      </h3>

      <div class="text-2xl mb-4">
        <span class="font-bold">Новые:</span>
        {{ numberWithCommas(stats.NewDeaths) }}
      </div>
      <div class="text-2xl mb-4">
        <span class="font-bold">Всего:</span>
        {{ numberWithCommas(stats.TotalDeaths) }}
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DataBoxes',
  props: ['stats'],
  methods: {
    numberWithCommas(x) {
      return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',');
    },
  },
};
</script>

<style></style>
