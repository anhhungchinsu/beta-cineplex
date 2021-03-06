<template>
    <div>
      <div class="slider mb-5">
        <div id="carouselExampleIndicators" class="carousel slide" data-ride="carousel">
          <ol class="carousel-indicators">
            <li data-target="#carouselExampleIndicators" data-slide-to="0" class="active"></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="1"></li>
            <li data-target="#carouselExampleIndicators" data-slide-to="2"></li>
          </ol>
          <div class="carousel-inner">
            <div class="carousel-item active">
              <img class="d-block w-100" src="../assets/img/slider1.jpg" alt="First slide">
            </div>
            <div class="carousel-item">
              <img class="d-block w-100" src="../assets/img/slider2.jpg" alt="Second slide">
            </div>
            <div class="carousel-item">
              <img class="d-block w-100" src="../assets/img/slider3.jpg" alt="Third slide">
            </div>
          </div>
          <a class="carousel-control-prev" href="#carouselExampleIndicators" role="button" data-slide="prev">
            <span class="carousel-control-prev-icon" aria-hidden="true"></span>
            <span class="sr-only">Previous</span>
          </a>
          <a class="carousel-control-next" href="#carouselExampleIndicators" role="button" data-slide="next">
            <span class="carousel-control-next-icon" aria-hidden="true"></span>
            <span class="sr-only">Next</span>
          </a>
        </div>
      </div>
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
  name: 'HomePage',
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
