<template>
    <div class="container">
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
                          <label class="control-label font-16">Email</label>
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
                              <button type="button" style="min-width: 220px;" id="btnLogin" onclick="login();" class="btn btn-success">
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
                          <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Họ tên</label>
                          <input type="text" style="height: 30px;" id="txtName" class="form-control" placeholder="Họ tên">
                      </div>
                      <div class="mb-4">
                          <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Email</label>
                          <div class="input-icon">
                              <i class="fa fa-envelope"></i>
                              <input type="text" style="height: 30px;" id="txtEmail" class="form-control" placeholder="Email">
                          </div>
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
                      <div class="mb-4">
                          <label class="control-label font-16"><span style="color: red;">*</span>&nbsp;Xác nhận lại mật khẩu</label>
                          <div class="input-icon">
                              <i class="fa fa-lock"></i>
                              <input type="password" style="height: 30px;" id="txtXacNhanMatKhau" class="form-control" placeholder="Xác nhận lại mật khẩu">
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
                          <label class="control-label font-16">Giới tính</label>
                          <div class="input-icon">
                              <i class="fa fa-male"></i>
                              <select id="cboSex" style="height: 30px;" class="form-control" data-placeholder="Giới tính" tabindex="1">
                                  <option class="option-item" value="0">Giới tính</option>
                                  <option class="option-item" value="1">Nam</option>
                                  <option class="option-item" value="2">Nữ</option>
                                  <option class="option-item" value="3">Khác</option>
                              </select>
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
                              <button type="button" style="min-width: 220px;" onclick="dangKy();" class="btn btn-success">
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
</template>

<script>

export default {
  name: 'RegisterPage',
  data() {
    return {
      currentButton: 1
    }
  },
  methods: {
    selectButton(b) {
      this.currentButton = b
    }
  }
}
</script>

<style>
  .back-gray {
    background-color: #F8F8F8;
  }
</style>
