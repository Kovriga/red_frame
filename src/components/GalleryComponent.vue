<template>
  <div class="gallery">
    <div class="button-location-in-image" @click="closeGallery()">
      <div>
        <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
          <path
              d="M10 0C4.42857 0 0 4.42857 0 10C0 15.5714 4.42857 20 10 20C15.5714 20 20 15.5714 20 10C20 4.42857 15.5714 0 10 0ZM13.8571 15L10 11.1429L6.14286 15L5 13.8571L8.85714 10L5 6.14286L6.14286 5L10 8.85714L13.8571 5L15 6.14286L11.1429 10L15 13.8571L13.8571 15Z"
              fill="#00D56A"/>
        </svg>
      </div>
    </div>
    <div class="gallery-item">
      <div class="button" @click="before()">
        <svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
             x="0px" y="0px"
             viewBox="0 0 199.227 199.227" style="enable-background:new 0 0 199.227 199.227;" xml:space="preserve" width="100px" height="100px" transform='rotate(270)'>
<g>
	<g>
		<polygon style="fill:#00D56A;" points="51.582,71.541 55.397,75.367 96.915,33.849 96.915,170.407 102.312,170.407
			102.312,33.849 143.823,75.367 147.645,71.541 99.61,23.517 		"/>
	</g>
</g>
</svg>
      </div>
      <div class="gallery-content">
        <img :src="titleComponent[ticket].path">
      </div>
      <div @click="netx()" class="button">
        <svg version="1.1" id="Capa_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink"
             x="0px" y="0px"
             viewBox="0 0 199.227 199.227" style="enable-background:new 0 0 199.227 199.227;" width="100px" height="100px" xml:space="preserve" transform='rotate(90)'>
<g>
	<g>
		<polygon style="fill:#00D56A;" points="51.582,71.541 55.397,75.367 96.915,33.849 96.915,170.407 102.312,170.407
			102.312,33.849 143.823,75.367 147.645,71.541 99.61,23.517 		"/>
	</g>
</g>
</svg>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {Options, prop, Vue} from "vue-class-component";


class Props {
  titleComponent: never = prop({
    required: true,
  });
}

@Options({})

export default class GalleryComponent extends Vue.with(Props) {

  lenghtImg = 0;
  ticket = 0;

  created(): void {
    this.lenghtImg = this.titleComponent.length;
  }

  before(): void {
    this.ticket = this.ticket - 1;
    if (this.ticket < 0) {
      this.ticket = this.titleComponent.length - 1;
    }
  }

  netx(): void {
    this.ticket = this.ticket + 1;
    if (this.ticket >= this.lenghtImg) {
      this.ticket = 0;
    }
  }

  closeGallery(): void {
    this.$emit('closeGallery', null)
  }
}
</script>

<style scoped lang="scss">
.button {
  display: flex;
  height: 100vh;
  width: 100px;
  justify-content: center;
  align-items: center;
}

.button > svg {
  color: white;
}

.gallery-content > img {
  max-width: 37%;
}

.gallery-content {
  height: 100vh;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}

.gallery-item {
  flex: auto;
  display: flex;
  justify-content: space-between;
}

.gallery {
  z-index: 2;
  top: 0;
  left: 0;
  position: absolute;
  width: 100%;
  margin: 0;
  height: 100vh;
  background-color: rgba(1, 0, 44, 0.76);
}

.button-location-in-image {
  display: flex;
  width: 48px;
  height: 48px;
  background: #FFFFFF;
  border: 2px solid #00D56A;
  border-radius: 8px;
  justify-content: center;
  align-items: center;
  position: absolute;
  right: 16px;
  top: 20px;
}
</style>