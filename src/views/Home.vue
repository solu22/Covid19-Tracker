<template>
<main v-if="!loading">
  <DataTitle :text= "title" :dataDate= "dataDate" />
  <DataTable :stats = "stats" />
</main>

<main class= "flex flex-col align-center justify-center text-center" v-else>
  <div class="text-gray-500 text-3xl mt-10 mb-6">
    Loading
  </div>
</main>
</template>

<script>
// @ is an alias to /src
import DataTitle from '@/components/DataTitle'
import DataTable from '@/components/DataTable'


export default {
  name: 'Home',
  components:  {
    DataTitle, DataTable
  },
  data(){
    return {
      loading: true,
      title: 'Global',
      dataDate: '',
      stats: {},
      countries: [],
    
    }
  },
  methods: {
    async fetchCovidData(){
      const res = await fetch('https://api.covid19api.com/summary')
      const data = await res.json()
      return data
    }
  },
  async created(){
    const data = await this.fetchCovidData()
    this.dataDate = data.dataDate
    this.stats = data. Global
    this.countries = data.countries
    this.loading = false
  }
}
</script>
