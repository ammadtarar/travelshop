<template>
  <div class="ratings-container">
    <div class="ratings">
      <div class="cell overall">
        <img src="../assets/ic_overall.svg" />
        <div class="info">
          <span class="title">Overall Rating</span>
          <span class="desc">{{ ratings.overall.rating }}</span>
        </div>

        <div class="score-container">
          <span class="score"> {{ ratings.overall.score }} </span>
          <img src="../assets/ic_star.png" alt="" class="star" />
        </div>
      </div>

      <div class="others">
        <div class="cell" v-for="item in ratings.others" v-bind:key="item.name">
          <img :src="require(`../assets/${item.icon}`)" />
          <div class="info">
            <span class="title">{{ item.name }}</span>
            <span class="desc">{{ item.rating }}</span>
          </div>

          <div class="score-container">
            <span class="score"> {{ item.score }} </span>
            <img src="../assets/ic_star.png" alt="" class="star" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ServiceRatings",
  props: ["ratings"],
};
</script>

<style lang="scss" scoped>
.ratings-container {
  width: 100%;
  background: white;
  margin-top: 2rem;

  .ratings {
    width: 100%;
    display: flex;
    flex-direction: column;
    border-radius: 1rem;
    overflow: hidden;

    .overall {
      background: rgba(48, 117, 157, 0.1) !important;
    }

    .others {
      width: 100%;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 0.1rem;
    }
    .cell {
      display: flex;
      flex-direction: row;
      align-items: center;
      background: #f6f7f9;
      padding: 1rem 2rem;
      background: rgba(48, 117, 157, 0.05);
      img {
        width: 2rem;
        margin-right: 2rem;
      }

      .info {
        display: flex;
        flex-direction: column;
        color: #2c3e50;
        font-size: 1.6rem;

        .title {
          font-weight: 700;
        }

        .desc {
          font-weight: 400;
        }
      }

      .score-container {
        margin-left: auto;
        display: flex;
        justify-content: center;
        align-items: center;

        .score {
          font-size: 1.6rem;
          font-weight: 700;
        }

        .star {
          width: 1.8rem;
          height: 1.8rem;
          margin-left: 1rem;
        }
      }
    }
  }
}

@media screen and (max-width: 480px) {
  .others {
    grid-template-columns: 1fr !important;
  }
}
</style>