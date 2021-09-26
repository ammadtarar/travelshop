<template>
  <div class="itineraries">
    <button @click="onClickExpandAll">
      {{ isExpandingAll ? "Hide All" : "Expand All" }}
    </button>

    <div class="items">
      <div class="item" v-for="(item, index) in items" v-bind:key="item.title">
        <div class="top" @click="onClickItem(index)">
          <img
            class="day-icon"
            :src="require(`../assets/${getItemIcon(index)}`)"
            :class="{ expandedIcon: item.isExpanding }"
          />
          {{ item.title }}
          <img
            src="../assets/ic_arrow_down.svg"
            class="arrow"
            :class="{ expandedArrow: item.isExpanding }"
          />
        </div>
        <transition name="fade">
          <p v-if="item.isExpanding" class="desc">{{ item.desc }}</p>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Itinerary",
  props: ["data"],
  data() {
    return {
      items: [],
      isExpandingAll: false,
    };
  },
  methods: {
    onClickExpandAll() {
      this.isExpandingAll = !this.isExpandingAll;
      this.items.forEach((item) => {
        item.isExpanding = this.isExpandingAll;
      });
    },
    getItemIcon(index) {
      if (index === 0) {
        return "ic_start_loc.svg";
      } else if (index === this.data.length - 1) {
        return "ic_end_loc.svg";
      } else {
        return "ic_mark.svg";
      }
    },
    onClickItem(index) {
      this.items[index].isExpanding = !this.items[index].isExpanding;
    },
  },
  mounted() {
    this.items = this.data;
  },
};
</script>

<style lang="scss" scoped>
.itineraries {
  width: 100%;
  margin-top: 1rem;
  display: flex;
  flex-direction: column;

  button {
    font-weight: 700;
    color: #0a7bbd;
    padding: 1.2rem;
    font-size: 1.6rem;
    background: transparent;
    border: none;
    margin-left: auto;
    margin-bottom: 1rem;
  }

  .items {
    width: 100%;
    display: flex;
    flex-direction: column;
    transition: all 0.3s ease-in-out;

    .item {
      width: 100%;
      display: flex;
      flex-direction: column;
      border-bottom: 0.1rem solid lightgray;
      padding-bottom: 1rem;
      transition: all 0.3s ease-in-out;

      .top {
        display: flex;
        align-items: center;
        font-weight: 700;
        color: black;
        font-size: 1.6rem;
        height: 5rem;

        .day-icon {
          width: 2rem;
          height: 2rem;
          margin-right: 1rem;
          transition: all 0.3s ease-in-out;
        }

        .expandedIcon {
          transform: scale(1.4);
        }

        .arrow {
          width: 1.6rem;
          height: 1.6rem;
          margin-left: auto;
          transition: all 0.3s ease-in-out;
        }

        .expandedArrow {
          transform: rotate(180deg);
        }
      }

      .desc {
        color: #2c3e50;
        font-weight: 400;
        font-size: 1.6rem;
      }
    }
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>