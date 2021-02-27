<template>
    <div class="container">
      <div class="row">
          <div class="col-12">
              <h2 class="text-left mt-5">Giá vé rạp {{selectedCinema.cinema_name}}</h2>
              <img class="img-fluid mb-5" src="https://files.betacorp.vn/files/ecm/2021/01/28/1920x2400-bang-gia-my-dinh-155727-280121-78.jpg" alt="">
          </div>
      </div>
    </div>
</template>

<script>

export default {
  name: 'TicketPage',
  props: {
    selectedCinema : {
        type: Object,
        default: null
    }
  }
}
</script>
