<template>
  <html>

  <body>
    <section>
      <div class="wrapper">
        <div class="row">
        <input type="color" class="light" value="#ffffff">
        <input type="color" class="dark" value="#ffffff">
        <select v-model="optionSelected" class="sizes" @change="test">
          <option disabled value="" style="padding-top: 5px;">Please, select one</option>
          <option style="padding-top: 10px;">100 px</option>
          <option style="padding-top: 10px;">200 px</option>
          <option style="padding-top: 10px;">300 px</option>
          <option style="padding-top: 10px;">400 px</option>
          <option style="padding-top: 10px;">500 px</option>
          <option style="padding-top: 10px;">600 px</option>
          <option style="padding-top: 10px;">700 px</option>
          <option style="padding-top: 10px;">800 px</option>
          <option style="padding-top: 10px;">900 px</option>
          <option style="padding-top: 10px;">1000 px</option>
        </select>
      </div>
      <input type="text" class="qr-text" placeholder="Enter QR Text">
      <div id="qr-code"></div>
      <div class="action-container"></div>
      <a href="#" class="download btn" download="QRcode">
        <span>Download</span>
        <img src="download.svg" alt="">
      </a>
      <button type="button" class="btn share-btn">
        <span>Share</span>
        <img src="share.svg" alt="">
      </button>
      </div>
      
    </section>
  </body>

</html>
</template>

<script>

export default {
  name: 'QRCodeGeneratorComponent',
  components: {},
  props: [],
  data() {
    return {
      optionSelected: '',
    }
  },
  methods: {
    test() {

    }
  }
}

</script>

<style scoped></style>
