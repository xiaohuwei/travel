<template>
    <div>
        <city-header></city-header>
        <city-search :city="city"></city-search>
        <city-list :city="city" :hot="hotCity" :letter="letter"></city-list>
        <city-alpha :city="city" @change="handLetter"></city-alpha>
    </div>
</template>
<script>
import CityHeader from './city/Header'
import CitySearch from './city/Search'
import CityList from './city/List'
import CityAlpha from './city/Alphabet'
import axios from 'axios'
export default {
    name: 'City',
    components: {
        CityHeader,
        CitySearch,
        CityList,
        CityAlpha
    },
    data() {
        return {
            city: [], //存放城市
            hotCity: [],    //热门城市
            letter: ""  //存储右边点击的数字
        }
    },
    methods: {
        getCityInfo () {
            axios
            .get("https://www.easy-mock.com/mock/5caf195f214dd7060924ac91/travel/city")
            .then(res => {
                const data = res.data.data
                this.city = data.city
                this.hotCity = data.hotCity
            })
        },
        handLetter (letter) {
            this.letter = letter;
        }
    },
    mounted() {
        this.getCityInfo()
    }
}
</script>
<style lang="stylus" scoped>
    
</style>