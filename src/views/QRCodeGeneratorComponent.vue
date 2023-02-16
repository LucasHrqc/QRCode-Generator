<template>
  <html>

  <body>
    <section>
      <div class="wrapper">
        <div class="row">
          <input type="color" class="light" v-model="lightColor" @input="handleLightColor">
          <input type="color" class="dark" v-model="darkColor" @input="handleDarkColor">
          <select v-model="sizeSelected" class="sizes" @change="handleSize">
            <option disabled value="" style="padding-top: 5px;">Please, select one</option>
            <option style="padding-top: 10px;">100 px</option>
            <option style="padding-top: 10px;">200 px</option>
            <option style="padding-top: 10px;">300 px</option>
            <option style="padding-top: 10px;">400 px</option>
            <option style="padding-top: 10px;">500 px</option>
          </select>
        </div>
        <input type="text" class="qr-text" placeholder="Enter QR Text" v-model="qrText" @input="handleQRText">
        <div id="qr-code"></div>
        <div class="action-container">
          <a href="#" class="download btn" download="QRcode">
            <span>Download</span>
            <img src="download.svg" alt="">
          </a>
          <button type="button" class="btn share-btn" @click="handleShare">
            <span>Share</span>
            <img src="share.svg" alt="">
          </button>
        </div>
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
      lightColor: '#ffffff',
      darkColor: '#000000',
      sizeSelected: '',
      qrText: '',
    }
  },
  methods: {
    handleLightColor() {
      this.generateQR();
    },
    handleDarkColor() {
      this.generateQR();
    },
    handleSize() {
      this.generateQR();
    },

    async handleShare() {
      setTimeout(async () => {
        try {
          const base64url = await this.resolveDataUrl();
          const blob = await (await fecth(base64url)).blob();
          const file = new File([blob], "QRCode.png", {
            type: blob.type,

          });
          await navigator.share({
            files: [file],
            title: this.qrText,
          })
        } catch (error) {
          alert("Your browser doesn't support sharing");
        }
      }, 100);
    },

    handleQRText() {
      this.generateQR();
    },

    async generateQR() {
      const qrContainer = document.querySelector('#qr-code');
      const download = document.querySelector('.download');
      qrContainer.innerHTML = '';
      let size = this.sizeSelected.replace(' px', ''),
        text = this.qrText,
        colorLight = this.lightColor,
        colorDark = this.darkColor;
      new QRCode("qr-code", {
        text,
        height: size,
        width: size,
        colorLight,
        colorDark,
      });
      download.href = await this.resolveDataUrl();
    },

    resolveDataUrl() {
      return new Promise((resolve, reject) => {
        setTimeout(() => {
          const img = document.querySelector('#qr-code img');
          if (img.currentSrc) {
            resolve(img.currentSrc);
            return
          }
          const canvas = document.querySelector('canvas');
          resolve(canvas.toDataURL());
        }, 50);
      })
    }
  }
}

</script>

<style scoped></style>
