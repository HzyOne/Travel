<template>
    <div>
        <city-header></city-header>
        <city-search :cities="cities"></city-search>
        <city-list
          :cities="cities"
          :hot="hotCities"
          :letter="letter"
        >
        </city-list>
        <city-alphabet
          :cities="cities"
          @change="handleLetterChange"
          >
        </city-alphabet>
    </div>
</template>

<script>
import axios from 'axios'
import CityHeader from './commpents/Header'
import CitySearch from './commpents/Search'
import CityList from './commpents/List'
import CityAlphabet from './commpents/Alphabet'

export default {
  name: 'City',
  components: {
    CityHeader: CityHeader,
    CitySearch: CitySearch,
    CityList: CityList,
    CityAlphabet: CityAlphabet
  },
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    handleLetterChange (letter) {
      this.letter = letter
    }
  },
  mounted () {
    this.getCityInfo()
  }
}
</script>

<style lang="stylus" scoped>

</style>
