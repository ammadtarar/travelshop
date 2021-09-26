<template>
  <div class="icon-btn">
    <img :src="require(`../assets/${icon}`)" alt="" />
    {{ title }}
  </div>
</template>

<script>
export default {
  name: "IconButton",
  props: ["title", "icon"],
};
</script>

<style lang="scss" scoped>
.icon-btn {
  width: 100%;
  display: flex;
  align-items: center;
  color: #0a7bbd;
  font-weight: 700;
  font-size: 1.6rem;
  justify-content: center;
  img {
    height: 2.4rem;
    height: 2.4rem;
    margin-right: 1rem;
  }
}

@media screen and (max-width: 480px) {
  .icon-btn {
    justify-content: left;
    height: 4rem;
  }
}
</style>