<template>
  <div class="reviews-container">
    <div class="sorting-actions">
      <button
        :class="{ selected: sortBy === 'recent' }"
        @click="sortBy = 'recent'"
      >
        Most Recent
      </button>
      <button
        :class="{ selected: sortBy === 'popular' }"
        @click="sortBy = 'popular'"
      >
        Most Popular
      </button>
      <button
        :class="{ selected: sortBy === 'highest' }"
        @click="sortBy = 'highest'"
      >
        Highest Rating
      </button>
      <button
        :class="{ selected: sortBy === 'lowest' }"
        @click="sortBy = 'lowest'"
      >
        Lowest Rating
      </button>
    </div>

    <div class="reviews">
      <div class="review" v-for="(review, index) in reviews" v-bind:key="index">
        <div class="top">
          <span class="initial">{{ review.name[0] }}</span>
          <div class="top-info">
            <div class="info">
              <span class="name">{{ review.name }}</span>
              <span class="date">{{ review.createdAt }}</span>
            </div>

            <div class="rating-container">
              <img
                src="../assets/ic_star.png"
                class="star"
                v-for="index in review.rating"
                v-bind:key="index"
              />
            </div>
          </div>
        </div>
        <p class="comment">{{ review.comment }}</p>
        <span class="trip-date">{{ review.tripDate }}</span>
        <div class="likes-container">
          <div class="action" @click="review.likes = review.likes + 1">
            <img src="../assets/ic_like.svg" />
            {{ review.likes }}
          </div>
          <div class="action" @click="review.dislikes = review.dislikes + 1">
            <img
              src="../assets/ic_like.svg"
              style="transform: rotate(180deg)"
            />
            {{ review.dislikes }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Reviews",
  props: ["reviews"],
  data() {
    return {
      sortBy: "recent",
    };
  },
  mounted() {
    console.log("reviewas");
    console.log(this.reviews);
  },
};
</script>

<style lang="scss" scoped>
.reviews-container {
  width: 100%;
  margin-top: 4rem;
  margin-bottom: 3rem;

  .sorting-actions {
    width: 100%;
    display: flex;
    transition: 0.2s all ease-in-out;

    button {
      background: transparent;
      border: 0.1rem solid #286283;
      color: #286283;
      font-size: 1.4rem;
      padding: 0.6rem 0.8rem;
      border-radius: 1.4rem;
      margin-right: 1rem;
      transition: 0.2s all ease-in-out;
    }

    :last-child {
      margin: 0rem;
    }

    .selected {
      background: #286283;
      color: white;
      font-weight: 700;
    }
  }

  .reviews {
    display: flex;
    flex-direction: column;
    margin-top: 1rem;

    .review {
      width: 100%;
      padding: 2rem 0rem;
      border-bottom: 0.1rem solid lightgray;

      .top {
        width: 100%;
        display: flex;
        flex-direction: row;
        align-items: center;

        .initial {
          width: 5rem;
          height: 5rem;
          display: flex;
          justify-content: center;
          align-items: center;
          color: white;
          font-size: 1.6rem;
          font-weight: 700;
          background: #286283;
          border-radius: 50%;
          margin-right: 1rem;
        }

        .top-info {
          display: flex;
          flex-direction: column;

          .info {
            .name {
              font-size: 1.6rem;
              font-weight: 700;
            }

            .date {
              font-size: 1.6rem;
              color: gray;
              margin-left: 1rem;
            }
          }

          .rating-container {
            display: flex;
            margin-left: -0.4rem;

            .star {
              width: 2rem;
              height: 2rem;
            }
          }
        }
      }

      .comment {
        font-size: 1.6rem;
        color: gray;
        margin: 1rem 0rem;
        font-weight: 300;
      }

      .trip-date {
        font-size: 1.4rem;
        color: gray;
        margin-top: 1rem;
        font-weight: 300;
      }

      .likes-container {
        display: flex;
        margin-top: 2rem;

        .action {
          border: 0.1rem solid #818d99;
          padding: 0.6rem 1.2rem;
          border-radius: 0.4rem;
          display: flex;
          justify-content: center;
          align-items: center;
          font-size: 1.6rem;
          color: #818d99;

          img {
            width: 2rem;
            height: 2rem;
            margin-right: 1rem;
          }
        }

        :first-child {
          margin-right: 1rem;
        }
      }
    }
  }
}
</style>