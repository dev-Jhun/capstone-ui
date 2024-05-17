<template>
    <v-data-table
      :headers="headers"
      :items="crop"
      :items-per-page="10"
      class="elevation-1"
    ></v-data-table>
  </template>
  <script>
  export default {
    data () {
      return {
        headers: [
          {
            text: 'CROP NAME',
            align: 'start',
            sortable: false,
            value: 'name',
          },
          { text: 'CROP VARIATION', value: 'var' },
          { text: 'SUGGESTED TEMPERATURE', value: 'temp' },
          { text: 'SUGGESTED HUMIDITY', value: 'humid' },
          { text: 'SUGGESTED PH', value: 'ph' },
          { text: 'SUGGESTED TDS', value: 'tds' },
          { text: 'SUGGESTED WATER TEMPERATURE', value: 'watertemp' },
        ],
        crop: [
          {
            name: 'Lettuce',
            var: 'Dabi',
            temp: 26,
            humid: 50,
            ph: 7,
            tds: 800,
            watertemp: 26,
          },
          {
            name: 'Lettuce',
            var: 'Olmetie',
            temp: 25,
            humid: 60,
            ph: "6 - 7",
            tds: "600 - 800",
            watertemp: "24 - 28",
          },
          {
            name: 'Lettuce',
            var: 'romaine',
            temp: 26,
            humid: 50,
            ph: 7,
            tds: 800,
            watertemp: 26,
          },
          {
            name: 'Cabbage',
            var: '',
            temp: 18,
            humid: 0,
            ph: '6 - 7',
            tds: 1750,
            watertemp: 0,
          },
          {
            name: 'Broccoli',
            var: '',
            temp: '16 - 21',
            humid: 0,
            ph: '6 - 6.5',
            tds: 1960,
            watertemp: 0,
          },
          {
            name: 'Cauliflower',
            var: '',
            temp: 24,
            humid: 0,
            ph: '6 - 7',
            tds: 1050,
            watertemp: 0,
          },
          {
            name: 'Celery',
            var: '',
            temp: 18,
            humid: 0,
            ph: '6 - 7',
            tds: 1260,
            watertemp: 0,
          },
          {
            name: 'Petchay',
            var: '',
            temp: 25,
            humid: 0,
            ph: '5.5 - 6.5',
            tds: 600,
            watertemp: 0,
          },
          {
            name: '',
            var: '',
            temp: 0,
            humid: 0,
            ph: 0,
            tds: 0,
            watertemp: 0,
          },
          {
            name: '',
            var: '',
            temp: 0,
            humid: 0,
            ph: 0,
            tds: 0,
            watertemp: 0,
          },
          {
            name: 'Lettuce',
            var: 'Dabi',
            temp: 26,
            humid: 50,
            ph: 7,
            tds: 800,
            watertemp: 26,
          },
        ],
      }
    },
  }
</script>