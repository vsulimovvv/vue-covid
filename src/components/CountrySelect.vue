<template>
  <select
    @change="onChange"
    v-model="selected"
    class="form-select w-full block border p-3 rounded mb-10 cursor-pointer"
  >
    <option value="0">Выбериту страну</option>
    <option v-for="country in countries" :key="country" :value="country.ID">
      {{ country.Country }}
    </option>
  </select>
</template>

<script>
export default {
  name: 'CountrySelect',
  props: ['countries'],
  data() {
    return {
      selected: 0,
    };
  },
  methods: {
    onChange() {
      const country = this.countries.find(
        (country) => country.ID === this.selected
      );
      console.log(country);

      this.$emit('get-country', country);
    },
  },
};
</script>

<style></style>
