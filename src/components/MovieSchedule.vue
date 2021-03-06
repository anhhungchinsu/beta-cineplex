<template>
    <div>
      <div class="movie-container">
        <div class="container">
          <div class="row">
            <div class="col-12">
              <div class="menu text-center">
                <a v-for="item in getArrDate()" :key="item" :class="{ 'actived' : currentTab === getArrDate().indexOf(item) }" @click="selectTab(getArrDate().indexOf(item))" href="#">{{ item }}</a>
              </div>
            </div>
          </div>
          <div class="row my-5">
            <div v-for="movie in getListMovieByDay(getArrDate()[currentTab])" :key="movie.name" class="col-3 mb-5">
              <div class="movie-item pb-4 pr-4 pl-4">
                <img class="img-fluid" :src="movie.movie_image">
                <h5 @click="getDetailMovie(movie)" class="pt-1 font-weight-bold blue-text">{{movie.movie_name}}</h5>
                <p><b>Thể loại:</b>{{movie.movie_type}}</p>
                <p><b>Thời lượng:</b> {{movie.movie_time}}</p>
                <div>
                  <a @click="buyTicket(movie.movie_id)" href="#">Mua vé</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
</template>

<script>
import _ from 'lodash'


export default {
  name: 'MovieSchedule',
  props: {
    moviesCanBuy : {
      type: Array,
      default: null
    }
  },
  data() {
    return {
      currentTab : 0
    }
  },
  methods: {
    getArrDate() {
      let arr = []
      const day = 1000 * 60 * 60 * 24
      let now = new Date()
      for (let i = 0; i < 5; i++) {
        let d = new Date(now.setTime(now.getTime() + day))
        arr.push(d.toISOString().slice(0, 10))
      }
      return arr
    },
    selectTab(tab) {
      this.currentTab = tab
    },
    getDetailMovie(movie) {
      this.$emit('getDetailMovie', movie)
    },
    getListMovieByDay(date) {
      return _.filter(this.moviesCanBuy, item => {
        let d = new Date(item.movie_start_date)
        const day = 1000 * 60 * 60 * 24
        d = new Date(d.setTime(d.getTime() + day)).toISOString().slice(0, 10)
        return d === date
      })
    },
    buyTicket(movieId) {
      this.$emit('buyTicket', movieId)
    }
  },
  computed: {
    
  }
}
</script>
