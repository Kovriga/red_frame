<template>
  <div class="main-component">
    <progress-spin v-if="spinVisible"></progress-spin>
    <div v-else>
      <div v-for="(item, index) in allPost" :key="index" class="main-component--item">
        <div class="main-component--item-image">
          <div class="button-location-in-image" @click="galleryVisible = item.id">
            <div>
              <svg width="22" height="20" viewBox="0 0 22 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M11.0001 14.6664C12.9441 14.6664 14.5201 13.0746 14.5201 11.1109C14.5201 9.14721 12.9441 7.55534 11.0001 7.55534C9.05601 7.55534 7.48005 9.14721 7.48005 11.1109C7.48005 13.0746 9.05601 14.6664 11.0001 14.6664Z" fill="white"/>
                <path d="M7.7 0L5.687 2.22222H2.2C0.99 2.22222 0 3.22222 0 4.44444V17.7778C0 19 0.99 20 2.2 20H19.8C21.01 20 22 19 22 17.7778V4.44444C22 3.22222 21.01 2.22222 19.8 2.22222H16.313L14.3 0H7.7ZM11 16.6667C7.964 16.6667 5.5 14.1778 5.5 11.1111C5.5 8.04445 7.964 5.55556 11 5.55556C14.036 5.55556 16.5 8.04445 16.5 11.1111C16.5 14.1778 14.036 16.6667 11 16.6667Z" fill="white"/>
              </svg>

            </div>
          </div>
          <div class="main-component--item-image-main">
            <img :src="item.images[0].path"
                 width="412" height="240">
          </div>
          <div class="main-component--item-image-child">
            <img :src="itemPhoto.path" width="162" height="112" v-for="(itemPhoto, index2) in item.images"
                 :key="index2">
          </div>
        </div>
        <div v-if="mapVisible === item.id" class="map">
          <div class="button-location-in-map" @click="mapVisibleEdit(item.id)">
            <div>
              <svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg">
                <path d="M10 0C4.42857 0 0 4.42857 0 10C0 15.5714 4.42857 20 10 20C15.5714 20 20 15.5714 20 10C20 4.42857 15.5714 0 10 0ZM13.8571 15L10 11.1429L6.14286 15L5 13.8571L8.85714 10L5 6.14286L6.14286 5L10 8.85714L13.8571 5L15 6.14286L11.1429 10L15 13.8571L13.8571 15Z" fill="#00D56A"/>
              </svg>
            </div>
          </div>
          <iframe :src="'https://yandex.ru/map-widget/v1/?ll='+item.l2+','+item.l1+'&pt='+item.l2+','+item.l1+'&sll='+item.l2+','+item.l1+'&z=17.09'" width="100%" height="100%" frameborder="0"></iframe>
        </div>
        <div v-else class="main-component--item-content">
          <div class="main-component--item-content--header">
            <div>
              <h3>{{ item.name }}</h3>
              <p>{{ item.address }}</p>
            </div>
            <div class="button-location" @click="mapVisibleEdit(item.id)">
              <div>
                <svg width="18" height="24" viewBox="0 0 18 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                  <path fill-rule="evenodd" clip-rule="evenodd"
                        d="M9 24C9 24 18 15.471 18 9C18 6.61305 17.0518 4.32387 15.364 2.63604C13.6761 0.948211 11.3869 0 9 0C6.61305 0 4.32387 0.948211 2.63604 2.63604C0.948211 4.32387 3.55683e-08 6.61305 0 9C0 15.471 9 24 9 24ZM9 13.5C10.1935 13.5 11.3381 13.0259 12.182 12.182C13.0259 11.3381 13.5 10.1935 13.5 9C13.5 7.80653 13.0259 6.66193 12.182 5.81802C11.3381 4.97411 10.1935 4.5 9 4.5C7.80653 4.5 6.66193 4.97411 5.81802 5.81802C4.97411 6.66193 4.5 7.80653 4.5 9C4.5 10.1935 4.97411 11.3381 5.81802 12.182C6.66193 13.0259 7.80653 13.5 9 13.5Z"
                        fill="white"/>
                </svg>
              </div>
            </div>
          </div>
          <div class="main-component--item-content--content">
            <div>
              <p>Занято номеров:</p>
              <p>Класс:</p>
              <p>Расположение</p>
            </div>
            <div>
              <p>{{ item.freeRooms }}/{{ item.allRooms }}</p>
              <p>{{ item.roomClass }}</p>
              <p>{{ item.distanceFromCenter }} км от центра</p>
            </div>
          </div>
          <div class="main-component--item-content--action">
            <p>от {{ item.sum.toLocaleString() }} р. за 1 день</p>
            <div class="button-info">
              <p>ПОДРОБНЕЕ</p>
            </div>
          </div>
        </div>
        <gallery-component @closeGallery="galleryVisibleFun" :titleComponent="item.images" v-if="galleryVisible === item.id"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import {Options, Vue} from "vue-class-component";
import GalleryComponent from "@/components/GalleryComponent.vue";
import ProgressSpin from "@/components/ProgressSpin.vue";
import DATA from "@/../db.json"

@Options({
  components: {ProgressSpin, GalleryComponent}
})

export default class MainComponent extends Vue {

  mapVisible: number | null = null;
  allPost: unknown[] = [];
  galleryVisible: number | null = null;
  spinVisible = true;

  galleryVisibleFun(item: null): void {
    this.galleryVisible = item;
  }

  async mounted (): Promise<void> {
    this.allPost = DATA.posts as unknown[];
    setTimeout(() => {
      this.spinVisible = false;
    }, 1000);
  }

  mapVisibleEdit(item: number): null | number {
    if (this.mapVisible === item) {
      return this.mapVisible = null;
    }
    return this.mapVisible = item;
  }
}
</script>

<style scoped lang="scss">
.button-location-in-image{
  display: flex;
  width: 48px;
  height: 48px;
  background: none;
  border: 2px solid white;
  border-radius: 8px;
  justify-content: center;
  align-items: center;
  position: absolute;
  left: 26px;
  bottom: 30px;
}
.button-location-in-map{
  display: flex;
  width: 48px;
  height: 48px;
  background: #FFFFFF;
  border: 2px solid #00D56A;
  border-radius: 8px;
  justify-content: center;
  align-items: center;
  position: absolute;
  left: 88%;
}
.map{
  position: relative;
  flex: auto;
  margin: 16px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.map > iframe {
  width: 100%;
  border-radius: 8px;
}
.main-component--item-content--action {
  display: flex;
  justify-content: space-between;
}

.main-component--item-content--action > p {
  font-family: 'Noto Sans';
  font-style: normal;
  font-weight: 700;
  font-size: 14px;
  line-height: 19px;
  display: flex;
  align-items: center;

  color: #01002C;
}

.button-info > p {
  font-family: 'Noto Sans';
  font-style: normal;
  font-weight: 700;
  font-size: 15px;
  line-height: 20px;
  text-align: center;
  color: white;
}

.button-info {
  display: flex;
  width: 204px;
  height: 48px;
  background: #00D56A;
  border-radius: 8px;
  justify-content: center;
  align-items: center;
}

.main-component--item-content--content > div {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

p {
  font-family: 'Noto Sans';
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 16px;
  color: #01002C;
  margin: 0;
}

h3 {
  margin: 0;
  font-family: 'Noto Sans';
  font-style: normal;
  font-weight: 400;
  font-size: 18px;
  line-height: 25px;
  display: flex;
  align-items: center;
  color: #00D56A;
}

.main-component--item-content--header {
  display: flex;
  justify-content: space-between;
}

.main-component--item-content--content {
  justify-content: space-evenly;
  display: flex;
  width: 410px;
  height: 100px;
  background: #F8F8FF;
  border-radius: 8px;
  margin: 8px 0 16px;
}

.main-component--item-content--header > div:first-child {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.button-location > div {
  display: flex;
  width: 48px;
  height: 48px;
  background: #00D56A;
  border-radius: 8px;
  justify-content: center;
  align-items: center;
}

.main-component--item-content {
  margin: 16px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.main-component--item-image {
  position: relative;
  display: flex;
}

.main-component--item-image > .main-component--item-image-child {
  display: flex;
  flex-direction: column;
}

.main-component--item-image > .main-component--item-image-child > img:first-child {
  display: none;
}

.main-component--item-image > .main-component--item-image-child > img:nth-child(2) {
  margin: 16px 0;

}

.main-component--item-image > div > img {
  border-radius: 8px;
}

.main-component--item-image > .main-component--item-image-main > img {
  margin: 16px;
}

.main-component--item {
  margin-top: 16px;
  display: flex;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 3px 4px 4px rgba(1, 0, 44, 0.25);
  max-width: 1052px;
  min-width: 400px;
}

.main-component {
  flex-direction: row-reverse;
  justify-content: center;
  margin: 0 16px 0 0;
  display: flex;
  height: 90%;
}

@media screen and (max-width: 1070px) {
  .main-component--item-image-child {
    display: none !important;
  }
}

@media screen and (max-width: 800px) {
  .main-component--item {
    width: 100%;
    flex-direction: column !important;
  }
}
</style>