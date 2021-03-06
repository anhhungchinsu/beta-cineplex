<template>
    <div>
      <div v-if="user === null" class="container">
        <div class="row justify-content-center my-5">
          <div class="col-6">
            <div class="row">
              <button class="col-6 btn rounded-0" :class="{ 'btn-primary' : currentButton === 1 }" @click="selectButton(1)">ĐĂNG NHẬP</button>
              <button class="col-6 btn rounded-0" :class="{ 'btn-primary' : currentButton === 2 }" @click="selectButton(2)">ĐĂNG KÝ</button>
            </div>
            <div v-if="currentButton === 1" class="row back-gray">
                <div class="col-12">
                  <div class="tab-pane active in" id="login">
                    <div class="form-group">
                        <div id="error-status" class="col-md-16 mb-4">
                            
                                                      
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group">
                        <div class="col-md-16 mb-4 text-left">
                            <label class="control-label font-16">Tên đăng nhập</label>
                            <div class="input-icon">
                                <i class="fa fa-user"></i>
                                <input type="text" id="txtLoginName" class="form-control" placeholder="Email">
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group">
                        <div class="col-md-16 margin-bottom-20 text-left">
                            <label class="control-label font-16">Mật khẩu</label>
                            <div class="input-icon">
                                <i class="fa fa-lock"></i>
                                <input type="password" id="txtLoginPassword" class="form-control" placeholder="Mật khẩu">
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group">
                        <div class="col-md-16 margin-bottom-20">
                            <a href="#doimatkhau-pop-up" class="fancybox-fast-view">
                                Quên mật khẩu?</a>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="clearfix"></div>
                    <div class="form-group">
                        <div class="col-md-16 text-center">
                            <div class="form-group">
                                <button @click="login()" type="button" style="min-width: 220px;" id="btnLogin" class="btn btn-success">
                                    Đăng nhập bằng tài khoản</button>
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group">
                        <div class="col-md-16 text-center">
                            <div class="form-group">
                                <button type="button" style="min-width: 220px;" onclick="loginByFacebook();" class="btn btn-info">
                                    
                                    Đăng nhập bằng Facebook</button>
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                  </div>
                </div>
            </div>
            <!-- ******************************************************************-->
            <div v-if="currentButton === 2" class="row back-gray">
                <div class="col-12 text-left mt-4">
                  <div class="row tab-pane active in" id="register">
                    <!-- BEGIN FORM-->
                    <div class="form-group col-6">
                        <div class="mb-4">
                            <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Tên đăng nhập</label>
                            <input type="text" style="height: 30px;" id="txtName" class="form-control" placeholder="Họ tên">
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group col-6">
                        <div class="mb-4">
                            <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Mật khẩu</label>
                            <div class="input-icon">
                                <i class="fa fa-lock"></i>
                                <input type="password" style="height: 30px;" id="txtMatKhau" class="form-control" placeholder="Mật khẩu">
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group col-6">
                        <div class="mb-4">
                            <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Ngày sinh</label>
                            <div class="input-icon">
                                <i class="fa fa-calendar"></i>
                                <input id="txtNgaySinh" style="height: 30px;" class="datepicker form-control" placeholder="Ngày sinh" data-date-format="dd/mm/yyyy">
                                
                            </div>
                        </div>
                        <div class="mb-4">
                            <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Địa chỉ</label>
                            <div class="input-icon">
                                <i class="fa fa-calendar"></i>
                                <input id="txtDiaChi" style="height: 30px;" class="datepicker form-control" placeholder="Địa chỉ">
                                
                            </div>
                        </div>
                    </div>
                    
                    <div class="clearfix"></div>
                    <div class="form-group col-6">
                        <div class="mb-4">
                            <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Số điện thoại</label>
                            <div class="input-icon">
                                <i class="fa fa-phone-square"></i>
                                <input type="text" style="height: 30px;" id="txtDienThoai" class="form-control" placeholder="Số điện thoại">
                            </div>
                        </div>
                        
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group col-12">
                        <div class="col-md-16">
                            <div class="form-group">
                                <input type="checkbox" id="chk" value="1">
                                <span style="display: normal"> Tôi cam kết tuân theo <a href="#chinhsachbaomat-pop-up" class="fancybox-fast-view">chính sách bảo mật</a> và <a href="#dieukhoansudung-pop-up" class="fancybox-fast-view">điều khoản sử dụng</a> của Betacineplex.
                                </span>
                                <span style="display: none">I have read and accecpt the <a href="#chinhsachbaomat-pop-up" class="fancybox-fast-view">Privacy policy</a> and <a href="#dieukhoansudung-pop-up" class="fancybox-fast-view">Terms and conditions</a> of Betacineplex.
                                </span>
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group col-6">
                        <div class="col-md-16 text-center">
                            <div class="form-group">
                                <button type="button" style="min-width: 220px;" @click="register();" class="btn btn-success">
                                    Đăng ký</button>
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <div class="form-group col-6">
                        <div class="col-md-16 text-center">
                            <div class="form-group">
                                <button type="button" style="min-width: 220px;" onclick="loginByFacebook();" class="btn btn-info">
                                    
                                    Tiếp tục với Facebook</button>
                            </div>
                        </div>
                    </div>
                    <div class="clearfix"></div>
                    <!-- END FORM-->
                  </div>
                </div>
              </div>
          </div>
        </div>
      </div>
      <div v-else class="container movie-container">
        <div class="row">
            <div class="col-12">
              <div class="menu text-center">
                <a :class="{ 'actived' : currentTab === 0 }" @click="selectTab(0)" href="#">Thông tin cá nhân</a>
                <a :class="{ 'actived' : currentTab === 1 }" @click="selectTab(1)" href="#">Vé đã mua</a>
              </div>
            </div>
        </div>
        <div v-if="currentTab === 0" class="row back-gray">
          <div class="col-12 text-left mt-4">
            <div class="row tab-pane active in" id="register">
              <!-- BEGIN FORM-->
              <div class="form-group col-6">
                  <div class="mb-4">
                      <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Tên đăng nhập</label>
                      <input type="text" style="height: 30px;" id="txtName" class="form-control" placeholder="Họ tên">
                  </div>
              </div>
              <div class="clearfix"></div>
              <div class="form-group col-6">
                  <div class="mb-4">
                      <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Mật khẩu</label>
                      <div class="input-icon">
                          <i class="fa fa-lock"></i>
                          <input type="password" style="height: 30px;" id="txtMatKhau" class="form-control" placeholder="Mật khẩu">
                      </div>
                  </div>
              </div>
              <div class="clearfix"></div>
              <div class="form-group col-6">
                  <div class="mb-4">
                      <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Ngày sinh</label>
                      <div class="input-icon">
                          <i class="fa fa-calendar"></i>
                          <input id="txtNgaySinh" style="height: 30px;" class="datepicker form-control" placeholder="Ngày sinh" data-date-format="dd/mm/yyyy">
                          
                      </div>
                  </div>
                  <div class="mb-4">
                      <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Địa chỉ</label>
                      <div class="input-icon">
                          <i class="fa fa-calendar"></i>
                          <input id="txtDiaChi" style="height: 30px;" class="datepicker form-control" placeholder="Địa chỉ">
                          
                      </div>
                  </div>
              </div>
              
              <div class="clearfix"></div>
              <div class="form-group col-6">
                  <div class="mb-4">
                      <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Số điện thoại</label>
                      <div class="input-icon">
                          <i class="fa fa-phone-square"></i>
                          <input type="text" style="height: 30px;" id="txtDienThoai" class="form-control" placeholder="Số điện thoại">
                      </div>
                  </div>
                  
              </div>
              <div class="clearfix"></div>
              <div class="form-group col-12">
                  <div class="col-md-16">
                      <div class="form-group">
                          <input type="checkbox" id="chk" value="1">
                          <span style="display: normal"> Tôi cam kết tuân theo <a href="#chinhsachbaomat-pop-up" class="fancybox-fast-view">chính sách bảo mật</a> và <a href="#dieukhoansudung-pop-up" class="fancybox-fast-view">điều khoản sử dụng</a> của Betacineplex.
                          </span>
                          <span style="display: none">I have read and accecpt the <a href="#chinhsachbaomat-pop-up" class="fancybox-fast-view">Privacy policy</a> and <a href="#dieukhoansudung-pop-up" class="fancybox-fast-view">Terms and conditions</a> of Betacineplex.
                          </span>
                      </div>
                  </div>
              </div>
              <div class="clearfix"></div>
              <div class="form-group col-6">
                  <div class="col-md-16 text-center">
                      <div class="form-group">
                          <button type="button" style="min-width: 220px;" @click="update();" class="btn btn-success">
                              Cập nhật</button>
                      </div>
                  </div>
              </div>
              <div class="clearfix"></div>
              <!-- END FORM-->
            </div>
          </div>
        </div>
        <div v-if="currentTab === 1" class="row">
          <table class="table table-bordered">
            <tr>
              <th>id</th>
              <th>tên phim</th>
              <th>giờ chiếu</th>
              <th>ngày mua vé</th>
            </tr>
            <tr v-for="item in tickets" :key="item.ticket_id">
              <th>{{item.ticket_id}}</th>
              <th>{{item.movie_name}}</th>
              <th>{{item.movie_showing_start_time}}</th>
              <th>{{item.ticket_date}}</th>
            </tr>
          </table>
        </div>
      </div>
    </div>
</template>

<script>
import axios from 'axios'
import $ from 'jquery'
import _ from 'lodash'


export default {
  name: 'RegisterPage',
  data() {
    return {
      currentButton: 1,
      currentTab: -1,
      tickets: [] 
    }
  },
  props: {
    user: {
      type: Object,
      default: null
    }
  },
  methods: {
    selectButton(b) {
      this.currentButton = b
    },
    login() {
      const username = $('#txtLoginName').val()
      const pass = $('#txtLoginPassword').val()
      axios.get(`http://localhost:3000/user`)
      .then(res => {
        const flag = _.findIndex(res.data, {
          'user_name' : username,
          'user_pass' : pass
        })
        if(flag != -1) {
          this.$emit('changeUser', res.data[flag])
        } else {
          alert("!ops")
        }
      })
    },
    register() {
      const username = $('#txtName').val()
      const pass = $('#txtMatKhau').val()
      const age = $('#txtNgaySinh').val()
      const phone = $('#txtDienThoai').val()
      const address = $('#txtDiaChi').val()
      axios.post(`http://localhost:3000/user`, {
        user_id : Math.floor(Math.random() * 9999),
        user_name : username,
        user_pass : pass,
        user_age : age,
        user_phone : phone,
        user_address : address,
        user_role : 'customer'
      })
      .then(res => {
        console.log(res)
        alert('Đăng ký thành công!')
      })
    },
    selectTab(tab) {
      if(tab === 0) {  
        this.currentTab = 0
        axios.get(`http://localhost:3000/user/${this.user.user_id}`)
        .then(res => {
          $('#txtName').val(res.data.user_name)
          $('#txtMatKhau').val(res.data.user_pass)
          $('#txtNgaySinh').val(res.data.user_age)
          $('#txtDienThoai').val(res.data.user_phone)
          $('#txtDiaChi').val(res.data.user_address)
        })
      }
      if(tab === 1) {
        this.currentTab = 1
        axios.get(`http://localhost:3000/ticket/user/${this.user.user_id}`)
        .then(res => {
          this.tickets = res.data
        })
      }
    },
    update() {
      const username = $('#txtName').val()
      const pass = $('#txtMatKhau').val()
      const age = $('#txtNgaySinh').val()
      const phone = $('#txtDienThoai').val()
      const address = $('#txtDiaChi').val()
      axios.put(`http://localhost:3000/user/${this.user.user_id}`, {
        user_name : username,
        user_pass : pass,
        user_age : age,
        user_phone : phone,
        user_address : address,
        user_role : 'customer'
      })
      .then(res => {
        console.log(res)
        alert('Cập nhật thành công!')
      })
    }
  }
}
</script>

<style>
  .back-gray {
    background-color: #F8F8F8;
  }
</style>
