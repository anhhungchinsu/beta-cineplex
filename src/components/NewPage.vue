<template>
    <div class="container">
      <div>
        <div class="row">
          <div class="col-6">
            <h2 class="my-2 text-left">KHUYẾN MÃI MỚI</h2>
            <div class="position-relative">
              <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/02/26/545x415-tb-mo-rap-100132-260221-61.jpg" alt="">
              <a @click="getDetailNew()" class="big-link" href="#">BETA QUANG TRUNG CHÍNH THỨC MỞ CỬA TRỞ LẠI TỪ 01/03/2021</a>
            </div>
          </div>
          <div class="col-6">
            <div class="row my-5">
              <div class="col-6">
                <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/02/25/545x415-gglc-100753-250221-73.jpg" alt="">
                <a @click="getDetailNew()" href="#">GÁI GIÀ LẮM CHIÊU V - SNEAK SHOW TỪ 5-8/3</a>
              </div>
              <div class="col-6">
                <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/01/27/545x415-qr-code-165146-270121-67.jpg" alt="">
                <a @click="getDetailNew()" href="#">QUÉT MÃ QR - 3 GIÂY THANH TOÁN</a>
              </div>
            </div>
          </div>
        </div>
        <div class="row my-5">
          <div class="col-3">
            <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/01/21/545x415-member-163558-210121-74.jpg" alt="">
            <a @click="getDetailNew()" href="#">THÀNH VIÊN BETA - ĐỒNG GIÁ 45K/50K</a>
          </div>
          <div class="col-3">
            <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/01/21/545x415-t3vv-1-164323-210121-12.jpg" alt="">
            <a @click="getDetailNew()" href="#">THỨ BA VUI VẺ</a>
          </div>
          <div class="col-3">
            <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/01/21/545x415-mad-sale-day-164833-210121-30.jpg" alt="">
            <a @click="getDetailNew()" href="#">SALE KHÔNG NGỪNG - MỪNG "MAD SALE DAY"</a>
          </div>
          <div class="col-3">
            <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/01/21/545x415-hssv-165349-210121-45.jpg" alt="">
            <a @click="getDetailNew()" href="#">GIÁ VÉ ƯU ĐÃI CHO HỌC SINH, SINH VIÊN</a>
          </div>
        </div>
      </div>
      <div>
        <div class="row">
          <div class="col-6">
            <h2 class="my-2 text-left">TIN BÊN LỀ</h2>
            <div class="position-relative">
              <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2020/11/30/545x415-174329-301120-64.jpg" alt="">
              <a @click="getDetailNew()" class="big-link" href="#">Beta Cinemas Giải Phóng - Khai trương 20/11/2020</a>
            </div>
          </div>
          <div class="col-6">
            <div class="row my-5">
              <div class="col-6">
                <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/02/25/545x415-gglc-100753-250221-73.jpg" alt="">
                <a @click="getDetailNew()" href="#">GÁI GIÀ LẮM CHIÊU V - SNEAK SHOW TỪ 5-8/3</a>
              </div>
              <div class="col-6">
                <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/02/22/untitled-3-171140-220221-57.jpg" alt="">
                <a @click="getDetailNew()" href="#">Tom & Jerry - Tượng Đài Tuổi Thơ Vừa Quen Vừa Lạ</a>
              </div>
            </div>
          </div>
        </div>
        <div class="row my-5">
          <div class="col-3">
            <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/02/22/545x415-beta-corona-jpg-173551-220221-29.jpg" alt="">
            <a @click="getDetailNew()" href="#">"Beta vs Corona" - Cuộc Chiến Chống Dịch Luôn Luôn Trong Tư Thế Sẵn Sàng</a>
          </div>
          <div class="col-3">
            <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/01/20/545x415-khai-truong-qt-102305-200121-73.jpg" alt="">
            <a @click="getDetailNew()" href="#">Beta Cinemas Quang Trung - Khai trương 22/1/2021</a>
          </div>
          <div class="col-3">
            <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2021/01/21/545x415-mad-sale-day-164833-210121-30.jpg" alt="">
            <a @click="getDetailNew()" href="#">SALE KHÔNG NGỪNG - MỪNG "MAD SALE DAY"</a>
          </div>
          <div class="col-3">
            <img class="img-fluid" src="https://files.betacorp.vn/files/ecm/2020/10/29/the-croods-2-141047-291020-78.jpg" alt="">
            <a @click="getDetailNew()" href="#">THE CROODS: A NEW AGE | 3 bom tấn hoạt hình không thể bỏ lỡ dịp cuối năm 2020</a>
          </div>
        </div>
      </div>
    </div>
</template>

<script>

export default {
  name: 'NewPage',
  methods: {
    getDetailNew() {
      this.$emit('getDetailNew')
    }
  }
}
</script>

<style scoped>
  .big-link {
    display: block;
    padding: 12px;
    background-color: orange;
    color: white;
    position: absolute;
    bottom: 0;
  }
</style>
