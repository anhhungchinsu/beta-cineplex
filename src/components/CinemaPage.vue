<template>
    <div class="container">
      <div class="row">
          <div class="col-6">
            <h3 class="text-left my-5">
                {{selectedCinema.cinema_name}}
            </h3>
            <img class="img-fluid mb-5" :src="selectedCinema.cinema_image" alt="">
            <p class="text-left">{{selectedCinema.cinema_post}}</p>
          </div>
          <div class="col-6">
            <h2 class="text-center my-5">
                <b>PHIM ĐANG HOT</b>
            </h2>
            <div class="my-5">
                <div class="row">
                  <div v-for="movie in moviesCanBuy" :key="movie.name" class="col-6 mb-5">
                    <div class="movie-item pb-4 pr-4 pl-4">
                        <img class="img-fluid" :src="movie.movie_image">
                        <h5 @click="getDetailMovie(movie)" class="pt-1 font-weight-bold blue-text">{{movie.movie_name}}</h5>
                        <p><b>Thể loại:</b>{{movie.movie_type}}</p>
                        <p><b>Thời lượng:</b> {{movie.movie_time}}</p>
                        <div>
                        <a class="btn btn-primary" href="#">Mua vé</a>
                        </div>
                    </div>
                  </div>
                </div>
            </div>
          </div>
      </div>
    </div>
</template>

<script>

export default {
  name: 'CinemaPage',
  props: {
    selectedCinema : {
        type: Object,
        default: null
    },
    moviesCanBuy : {
        type: Array,
        default: null
    }
  },
  methods: {
    getDetailMovie(movie) {
      this.$emit('getDetailMovie', movie)
    }
  }
}
</script>
