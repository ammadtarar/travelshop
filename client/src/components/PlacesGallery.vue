<template>
  <div class="places-gallery">
    <div class="places-gallery">
      <div class="inner" v-bind:id="name">
        <div class="place" v-for="place in places" v-bind:key="place">
          <div class="img-wrapper">
            <img :src="require(`../assets/images/${place.img}`)" />
          </div>
          {{ place.name }}
        </div>
      </div>
      <img
        src="../assets/ic_arrow_left.png"
        class="btn-nav left"
        @click="scrollGalleryLeft"
      />
      <img
        src="../assets/ic_arrow_right.png"
        class="btn-nav right"
        @click="scrollGalleryRight"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "PlacesGallery",
  props: ["places", "name"],
  methods: {
    scrollGalleryLeft() {
      let content = document.getElementById(this.name);
      content.scrollLeft -= 250;
    },
    scrollGalleryRight() {
      let content = document.getElementById(this.name);
      content.scrollLeft += 250;
    },
  },
};
</script>

<style lang="scss" scoped>
.places-gallery {
  margin-top: 2rem;
  width: 100%;
  height: 21rem;
  position: relative;
  margin-bottom: 3rem;

  .inner {
    width: 100%;
    height: 100%;
    z-index: 1;
    display: flex;
    overflow: auto;
    scroll-behavior: smooth;

    .place {
      min-width: 24rem;
      height: 100%;
      margin-right: 2rem;
      font-size: 1.6rem;
      font-weight: 700;

      .img-wrapper {
        width: 100%;
        height: 18.5rem;
        overflow: hidden;
        margin-bottom: 1rem;
        border-radius: 0.6rem;

        img {
          position: relative;
          width: 100%;
          height: 100%;
        }
      }
    }
  }

  .inner::-webkit-scrollbar {
    display: none;
  }
  img {
    z-index: 2;
    height: 5rem;
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
  }

  .left {
    left: -2.5rem;
  }
  .right {
    right: -2.5rem;
  }
}
</style>