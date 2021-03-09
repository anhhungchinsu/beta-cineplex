<template>
    <div>
      <div id="myModal" class="modal" tabindex="-1" role="dialog" data-backdrop="static">
        <div class="modal-dialog" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h5 class="modal-title">Chọn rạp</h5>
            </div>
            <div class="modal-body">
              <select class="custom-select" v-model="selectedAddress">
                <option disabled value="">Chọn tỉnh/thành phố</option>
                <option v-for="city in listAddress" :key="city.cinema_id">{{city.cinema_address}}</option>
              </select>
              <select class="custom-select" v-model="selectedName" @change="closeModal()">
                <option disabled value="">Chọn rạp</option>
                <option v-for="cinema in getListCinemaByAddress(selectedAddress)" :key="cinema.cinema_id">{{cinema.cinema_name}}</option>
              </select>
            </div>
          </div>
        </div>
      </div>
      <div v-if="user != null" id="ticketModal" class="modal bd-example-modal-lg" tabindex="-1" role="dialog" data-backdrop="static">
        <div class="modal-dialog modal-lg" role="document">
          <div class="modal-content">
            <div class="modal-header">
              <h1 class="modal-title"><img width="55" height="55" src="../assets/img/tickets.png" alt="">TICKETS</h1>
            </div>
            <div class="modal-body">
              <div class="row">
                <div class="col-6 text-left mb-3" style="border-right: 1px solid #20c997">
                  <h3>
                    CHI TIẾT PHIM
                  </h3>
                  <img width="150" class="img-thumbnail mb-3" :src="ticketMovie.movie_image" alt="">
                  <p><b>Tên phim:</b> {{ticketMovie.movie_name}}</p>
                  <p><b>Tác giả:</b> {{ticketMovie.movie_director}}</p>
                  <p><b>Thể loại:</b> {{ticketMovie.movie_type}}</p>
                  <p><b>Thời lượng:</b> {{ticketMovie.movie_time}}</p>
                  <p><b>Ngày công chiếu:</b> {{ticketMovie.movie_start_date}}</p>
                  <p><b>Giá vé:</b> <img src="../assets/img/free.png"></p>
                </div>
                <div class="col-6 text-left mb-3">
                  <h3>
                    THÔNG TIN 
                  </h3>
                  <p><b>Tên bạn:</b> {{user.user_name}}</p>
                  <p><b>Địa chỉ bạn:</b> {{user.user_address}}</p>
                  <p><b>Số điện thoại bạn:</b> {{user.user_phone}}</p>
                </div>
              </div>
              <p class="text-warning">Vé đã đặt vui lòng không trả lại</p>
              <p><span class="text-danger">Phim dành cho lứa tuổi 18+ </span>
                <br>Tôi cam kết tuân theo chính sách bảo mật và điều khoản sử dụng của Betacineplex.
              </p>
              <input type="checkbox" name="" id=""> Tôi đã hiểu
              <div class="modal-footer">
                <button @click="buy()" type="button" class="btn btn-primary">Đặt vé</button>
                <button type="button" class="btn btn-secondary" data-dismiss="modal">Hủy</button>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="header-pre">
          <div class="container">
              <div v-if="user === null" class="row">
                <div class="col-12 text-right">
                  <div class="pre-form">
                    <a @click="getCurrentPage(7)" href="#">Đăng nhập</a>
                    <span> | </span>
                    <a @click="getCurrentPage(7)" href="#">Đăng ký</a>
                  </div>
                </div>
              </div>
              <div v-else class="row">
                <div class="col-12 text-right">
                  <div class="pre-form">
                    <a @click="getCurrentPage(7)" href="#">{{user.user_name}}</a>
                    <span> | </span>
                    <a @click="logout()" href="#">Đăng Xuất</a>
                  </div>
                </div>
              </div>
          </div>
      </div>
      <div class="header">
        <div class="container">
          <div class="row">
            <div class="col-12 d-flex align-items-center">
              <a @click="getCurrentPage(0)" href="#"><img height="55" src="../assets/img/logo.png"></a>
              <div class="header-drop">
                <nav class="d-inline-block">
                  <ul id='menu'>
                    <li><a class='prett' href='#' title='Menu'>{{selectedName}}</a>
                      <ul class='menus'>
                        <li v-for="city in listAddress" :key="city.cinema_id" class='has-submenu'><a class='prett' href='Dropdown 2' title='Dropdown 2'>{{city.cinema_address}}</a>
                          <ul class='submenu'>
                            <li v-on:click="getShowingMovie(cinema)" v-for="cinema in getListCinemaByAddress(city.cinema_address)" :key="cinema.cinema_id"><a href="#" title="Sub Menu">{{cinema.cinema_name}}</a></li>
                          </ul>
                        </li>
                      </ul>
                    </li>
                  </ul>
                </nav>
              </div>
              <div class="header-menu">
                <ul>
                  <li><a @click="getCurrentPage(1)" href="#">lịch chiếu theo rạp</a></li>
                  <li><a @click="getCurrentPage(2)" href="#">phim</a></li> 
                  <li><a @click="getCurrentPage(3)" href="#">rạp</a></li>
                  <li><a @click="getCurrentPage(4)" href="#">giá vé</a></li>
                  <li><a @click="getCurrentPage(5)" href="#">tin mới và ưu đãi</a></li>
                  <li><a @click="getCurrentPage(6)" href="#">nhượng quyền</a></li>
                  <li><a @click="getCurrentPage(7)" href="#">thành viên</a></li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
      <template>
        <component :is="currentPage" :currentTab="currentTab" :movies="movies" :moviesCanBuy="moviesCanBuy" :movieDetail="movieDetail" :selectedCinema="selectedCinema" :user="user" @selectTab="selectTab" @getCurrentPage="getCurrentPage" @getDetailMovie='getDetailMovie' @getDetailNew="getDetailNew" @changeUser="changeUser" @buyTicket="buyTicket"></component>
      </template>
      
      <footer-page></footer-page>
    </div>
</template>

<script>
import FooterPage from '../components/FooterPage'
import HomePage from '../components/HomePage'
import MoviePage from '../components/MoviePage'
import MovieSchedule from '../components/MovieSchedule'
import MovieDetailPage from '../components/MovieDetailPage'
import CinemaPage from '../components/CinemaPage'
import TicketPage from '../components/TicketPage'
import NewPage from '../components/NewPage'
import NewDetailPage from '../components/NewDetailPage'
import FranchisePage from '../components/FranchisePage'
import RegisterPage from '../components/RegisterPage'
import axios from 'axios'
import $ from 'jquery'
import _ from 'lodash'

export default {
    name: "Home",
    components: {
      HomePage,
      FooterPage,
      MovieSchedule,
      MoviePage,
      MovieDetailPage,
      CinemaPage,
      TicketPage,
      NewPage,
      NewDetailPage,
      FranchisePage,
      RegisterPage
    },
    data() {
      return {
        movies: [],
        cinemas: [],
        listAddress: [],
        selectedCinema: null,
        selectedAddress: '',
        selectedName: '',
        currentTab: 2,
        moviesCanBuy: [],
        currentPage: "HomePage",
        movieDetail: null,
        user: null,
        ticketMovie: []
      }
    },
    methods: {
      getListMovie() {
        axios.get(`http://localhost:3000/movie`)
        .then(res => {
          this.movies = res.data
        })
      },
      async getShowingMovieByCinemaId(cinema) {
        return axios.get(`http://localhost:3000/movie_showing/cinema/${cinema.cinema_id}`)
        .then(res => {
          this.moviesCanBuy = res.data
        })
      },
      getListCinemaByAddress(address) {
        return _.filter(this.cinemas, item => item.cinema_address === address)
      },
      getShowingMovie(cinema) {
        this.currentTab = 2
        this.selectedCinema = cinema
        this.selectedName = cinema.cinema_name
        axios.get(`http://localhost:3000/movie`)
        .then(res => {
          let movie = res.data
          const today = new Date().toISOString().slice(0, 10)
          movie = JSON.parse(JSON.stringify(_.filter(movie, item => {
            let newDate = new Date(item.movie_start_date).toISOString().slice(0, 10) 
            return newDate === today 
          })))
          this.movies = movie
        })
      },
      getIncommingMovie() {
        this.currentTab = 1
        axios.get(`http://localhost:3000/movie`)
        .then(res => {
          let movie = res.data
          const today = new Date().toISOString().slice(0, 10)
          movie = JSON.parse(JSON.stringify(_.filter(movie, item => {
            let newDate = new Date(item.movie_start_date).toISOString().slice(0, 10) 
            return newDate > today 
          })))
          this.movies = movie
        })
      },
      async closeModal() {
        $(document).ready(()=>{
          $('#myModal').modal('hide')
        })
        const cinema = JSON.parse(JSON.stringify(_.filter(this.cinemas, item => item.cinema_name === this.selectedName )))
        this.selectedCinema = cinema[0]
        this.getShowingMovie(cinema[0])
        this.getShowingMovieByCinemaId(this.selectedCinema)
      },
      async selectTab(selectedTab) {
        this.currentTab = selectedTab
        if(selectedTab === 1) {
          this.getIncommingMovie()
        }
        if(selectedTab === 2) {
          this.getShowingMovie(this.selectedCinema)
        }
        if(selectedTab === 3) {
          this.movies = []
        }
      },
      getCurrentPage(page) {
        if(page === 1) {
          this.currentPage = "MovieSchedule"
          return
        }
        if(page === 2) {
          this.currentPage = "MoviePage"
          return
        }
        if(page === 3) {
          this.currentPage = "CinemaPage"
          return
        }
        if(page === 4) {
          this.currentPage = "TicketPage"
          return
        }
        if(page === 5) {
          this.currentPage = "NewPage"
          return
        }
        if(page === 6) {
          this.currentPage = "FranchisePage"
          return
        }
        if(page === 7) {
          this.currentPage = "RegisterPage"
          return
        }
        if(page === 10) {
          this.currentPage = "MovieDetailPage"
          return
        }
        if(page === 11) {
          this.currentPage = "NewDetailPage"
          return
        }
        this.currentPage = "HomePage"
        return
      },
      getDetailMovie(movie) {
        this.movieDetail = movie
        this.currentPage = "MovieDetailPage"
      },
      getDetailNew() {
        this.getCurrentPage(11)
        this.currentPage = "NewDetailPage"
      },
      changeUser(currentUser) {
        this.user = currentUser
      },
      logout() {
        this.user = null
      },
      buyTicket(movie) {
        if(this.user === null) {
          this.currentPage = "RegisterPage"
        } else {
          $(document).ready(()=>{
            $('#ticketModal').modal('show')
          })
          this.ticketMovie = movie
        }
      },
      buy() {
      axios.post(`http://localhost:3000/ticket`, {
        ticket_id : Math.floor(Math.random() * 9999),
        ticket_movie_showing_id : this.ticketMovie.movie_id,
        ticket_user_id : this.user.user_id,
        ticket_date : new Date().toISOString().slice(0, 10)
      })
      .then(res => {
        console.log(res)
        alert('Mua thành công!')
        $(document).ready(()=>{
          $('#ticketModal').modal('hide')
        })
      })
      }
    },
    created() {
      $(document).ready(()=>{
        $('#myModal').modal('show')
      })
    },
    mounted() {
      axios.get(`http://localhost:3000/cinema`)
      .then(res => {
        this.cinemas = res.data
        this.listAddress = _.uniqBy(res.data, 'cinema_address')
      })
    },
    watch: {
      selectedCinema() {
        this.getShowingMovieByCinemaId(this.selectedCinema)
      }
    }
}
</script>

<style lang="scss">
  .header-pre {
    background-color: black;
  }
  .pre-form {
    a {
      color: white;
      font-size: 12px;
    }
    span {
      color: white;
    }
  }
  .header {
    box-shadow: 0 1px 3px #ddd;
    padding: 5px 0;
  }
  #menu {
    color: black;
    height: 35px;
    display: inline-block;
  }

  #menu ul,
  #menu li {
    margin: 0 0;
    padding: 0 0;
    list-style: none
  }

  #menu ul {
    height: 35px
  }

  #menu li {
    float: left;
    display: inline;
    position: relative;
    font: bold 12px Arial;
    text-transform: uppercase;
    border-bottom: 1px solid #000;
  }

  #menu a {
    display: block;
    line-height: 35px;
    padding: 0 14px;
    text-decoration: none;
    color: black;
    white-space: nowrap;
  }

  #menu li:hover > a,
  #menu li a:hover {
    background: white
  }

  #menu input {
    display: none;
    margin: 0 0;
    padding: 0 0;
    width: 80px;
    height: 35px;
    opacity: 0;
    cursor: pointer
  }

  #menu label {
    font: bold 30px Arial;
    display: none;
    width: 35px;
    height: 36px;
    line-height: 36px;
    text-align: center
  }

  #menu label span {
    font-size: 12px;
    position: absolute;
    left: 35px
  }

  #menu ul.menus {
    height: auto;
    width: 180px;
    background: white;
    position: absolute;
    z-index: 99;
    display: none;
    border: 0;
  }

  #menu ul.menus li {
    display: block;
    width: 100%;
    font: 12px Arial;
    text-transform: none;
  }

  #menu li:hover ul.menus {
    display: block
  }

  #menu a.prett {
    padding: 0 27px 0 14px
  }

  #menu a.prett::after {
    content: "";
    width: 0;
    height: 0;
    border-width: 6px 5px;
    border-style: solid;
    border-color: #000 transparent transparent transparent;
    position: absolute;
    top: 15px;
    right: 9px
  }

  #menu ul.menus a:hover {
    background: #83BEE0 !important;
  }

  #menu ul.menus .submenu {
    display: none;
    position: absolute;
    left: 180px;
    background: white;
    top: 0;
    width: 180px;
  }

  #menu ul.menus .submenu li {
    background: white;
  }

  #menu ul.menus .has-submenu:hover .submenu {
    display: block;
  }
  .header-menu {
    margin-left: 30px;
    display: flex;
    ul {
      list-style: none;
      margin: 0;
      padding: 0;
      display: flex;
    }
    a {
      display: block;
      text-transform: uppercase;
      color: #000;
      padding: 0 6px;
      font-weight: bold;
      font-size: 17px;
      white-space: nowrap;
    }
    a:hover {
      text-decoration: none;
      color: #83BEE0 !important;
    }
  }
  .movie-container {
    .menu a {
      display: inline-block;
      color: #000;
      text-transform: uppercase;
      font-size: 30px;
      padding: 0 10px;
      border-bottom: 1px solid #ccc;
      &:hover {
        text-decoration: none;
      }
    }
    .actived {
      color: #03599d !important;
      border-bottom: 4px solid #03599d !important;
    }
    .movie-item {
      img {
        border-radius: 20px;
      }
      a {
        color: #fff;
        display: block;
        font-size: 18px;
        text-align: center;
        background: linear-gradient(to right, #0a64a7 0%, #258dcf 51%, #3db1f3 100%);
        border-radius: 4px;
        padding: 5px 0;
        &:hover {
          text-decoration: none;
          background: #0a64a7 !important;
        }
      }
    }
    h5:hover {
      cursor: pointer;
      color: #258dcf;
    }
    a:hover {
      cursor: pointer;
    }
    
  }
</style>

