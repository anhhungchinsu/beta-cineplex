<template>
    <div>
      <div class="movie-container">
        <div class="container">
          <h4 class="text-left font-bold my-5 actived">Trang chủ > {{movieDetail.movie_name}}</h4>
          <div class="row">
            <div class="col-3">
              <img class="img-fluid" :src="movieDetail.movie_image">
            </div>
            <div class="col-9">
              <h2 class="text-left">{{movieDetail.movie_name}}</h2>
              <p class="text-left">{{movieDetail.movie_description}}</p>
              <div class="d-flex flex-column align-items-start">
                <div class="row w-100 text-left">
                  <p class="col-4"><b>ĐẠO DIỄN:</b></p> 
                  <p class="col-8">{{movieDetail.movie_director}}</p>
                </div>
                <div class="row w-100 text-left">
                  <p class="col-4"><b>DIỄN VIÊN:</b></p> 
                  <p class="col-8">{{movieDetail.movie_actor}}</p>
                </div>
                <div class="row w-100 text-left">
                  <p class="col-4"><b>THỂ LOẠI:</b></p> 
                  <p class="col-8">{{movieDetail.movie_type}}</p>
                </div>
                <div class="row w-100 text-left">
                  <p class="col-4"><b>THỜI LƯỢNG:</b></p> 
                  <p class="col-8">{{movieDetail.movie_time}}</p>
                </div>
                <div class="row w-100 text-left">
                  <p class="col-4"><b>NGÔN NGỮ:</b></p> 
                  <p class="col-8">{{movieDetail.movie_language}}</p>
                </div>
                <div class="row w-100 text-left">
                  <p class="col-4"><b>NGÀY KHỞI CHIẾU:</b></p> 
                  <p class="col-8">{{movieDetail.movie_start_date}}</p>
                </div>
              </div>
            </div>
          </div>
          <div class="row my-5">
            <div class="col-12">
              <div class="menu text-left">
                <a v-for="item in listStartDate" :key="item" :class="{ 'actived' : currentDateTab === listStartDate.indexOf(item) }" @click="selectDate(listStartDate.indexOf(item), item)">{{ item }}</a>
              </div>
            </div>
          </div>
          <div class="row">
            <div v-for="(time, i) in getListTime()" :key="i" class="col-3 mb-5">
              <button class="btn btn-primary">{{new Date(time).toTimeString().slice(0, 8)}}</button>
            </div>
          </div>
        </div>
        <div class="container-fluid"  style="background: #3C3E4D;">
          <div class="container">
          <div class="embed-responsive embed-responsive-16by9">
            <iframe class="embed-responsive-item" :src="movieDetail.movie_trailer" allowfullscreen></iframe>
          </div>
        </div>
        </div>
        
      </div>
    </div>
</template>

<script>
import axios from 'axios'
import _ from 'lodash'

export default {
  name: 'MovieDetailPage',
  props: {
    movieDetail : {
      type: Object,
      default: null
    },
  },
  data() {
    return {
      listStartDate: [],
      listStartTime: [],
      currentDateTab: 0,
      currentDate: ''
    }
  },
  methods: {
    selectDate(dateTab, date) {
      this.currentDateTab = dateTab 
      this.currentDate = date
    },
    getListTime() {
      return _.filter(this.listStartTime, item => {
        return new Date(item).toISOString().slice(0, 10) === this.currentDate
      })
    }
  },
  mounted() {
    axios.get(`http://localhost:3000/movie_showing/movie/${this.movieDetail.movie_id}`)
      .then(res => {
        res.data.forEach(item => {
          this.listStartDate.push(new Date(item.movie_showing_start_time).toISOString().slice(0, 10))
          this.listStartTime.push(new Date(item.movie_showing_start_time))
        });
        this.listStartDate = _.uniq(this.listStartDate)
        this.currentDate = this.listStartDate[0]
    })
  }
}
</script>
