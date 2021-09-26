<template>
  <div class="main-container">
    <div class="img-wrapper">
      <img :src="require(`../assets/images/${this.images[index]}`)" alt="" />
    </div>
    <img
      src="../assets/ic_arrow_left.png"
      class="btn-nav left"
      @click="onClickBack"
    />
    <img
      src="../assets/ic_arrow_right.png"
      class="btn-nav right"
      @click="onClickNext"
    />
  </div>
</template>

<script>
export default {
  name: "ImagesSlide",
  props: ["images"],
  data() {
    return {
      index: 0,
    };
  },
  methods: {
    onClickNext() {
      this.index = this.index >= this.images.length - 1 ? 0 : this.index + 1;
    },
    onClickBack() {
      this.index = this.index <= 0 ? this.images.length - 1 : this.index - 1;
    },
  },
};
</script>

<style lang="scss" scoped>
.main-container {
  width: 100%;
  height: 45rem;
  position: relative;
  border-radius: 2rem;
  overflow: hidden;

  .img-wrapper {
    width: 100%;
    height: 100%;
    img {
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }

  .btn-nav {
    position: absolute;
    width: 5rem;
    height: 5rem;
    top: 50%;
    transform: translateY(-50%);
    border-radius: 50%;
    transition: 0.2s all ease-in-out;
    &:hover {
      box-shadow: 0rem 0rem 1rem 0rem lightgray;
      transform: scale(1.1) translateY(-2.2rem);
    }
  }

  .left {
    left: 2rem;
  }

  .right {
    right: 2rem;
  }
}

@media screen and (max-width: 480px) {
  .main-container {
    height: 25rem;
  }
}
</style>