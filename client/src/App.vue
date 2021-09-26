<template>
  <router-view />
</template>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: sans-serif;
}

:root {
  --transition: 0.2s all ease-in;

  //COLORS
  --clr-border: #ebeef2;
  --card-shadow: 0 1px 2px rgb(3 54 63 / 40%), 0 -1px 2px rgb(3 54 63 / 4%);

  // DIMENS
  --content-width: 75%;
}

html {
  scroll-behavior: smooth;
  font-size: 62.5%;
}

.hollow-btn {
  border-radius: 0.2rem;
  background: transparent;
  border: 0.1px solid #0a7bbd;
  color: #0a7bbd;
  font-weight: 700;
  font-size: 1.6rem;
  min-width: 17rem;
  transition: all 0.3s ease-in-out;

  &:hover {
    background: #0a7bbd;
    color: white;
  }
}
</style>
