<template>
    <div>
      <div class="movie-container">
        <div class="container">
          <div class="row">
            <div class="col-12">
              <div class="menu text-center">
                <a @click="selectTab(1)" :class="{ 'actived' : currentTab === 1 }" href="#">phim sắp chiếu</a>
                <a @click="selectTab(2)" :class="{ 'actived' : currentTab === 2 }" href="#">phim đang chiếu</a>
                <a @click="selectTab(3)" :class="{ 'actived' : currentTab === 3 }" href="#">suất chiếu đặc biệt</a>
              </div>
            </div>
          </div>
          <div class="row my-5">
            <div v-for="movie in movies" :key="movie.name" class="col-3 mb-5">
              <div class="movie-item pb-4 pr-4 pl-4">
                <img class="img-fluid" :src="movie.movie_image">
                <h5 @click="getDetailMovie(movie)" class="pt-1 font-weight-bold blue-text">{{movie.movie_name}}</h5>
                <p><b>Thể loại:</b>{{movie.movie_type}}</p>
                <p><b>Thời lượng:</b> {{movie.movie_time}}</p>
                <div v-if="checkCanBuy(movie.movie_name) > -1 ">
                  <a @click="buyTicket(movie)" href="#">Mua vé</a>
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
  name: 'MoviePage',
  props: {
    currentTab : {
      type: Number,
      default: 2
    },
    movies : {
      type: Array,
      default: null
    },
    moviesCanBuy : {
      type: Array,
      default: null
    }
  },
  methods: {
    checkCanBuy(movieName) {
      return _.findIndex(this.moviesCanBuy, ['movie_name', movieName])
    },
    selectTab(tab) {
      this.$emit('selectTab', tab)
    },
    getDetailMovie(movie) {
      this.$emit('getDetailMovie', movie)
    },
    buyTicket(movieId) {
      this.$emit('buyTicket', movieId)
    }
  }
}
</script>
