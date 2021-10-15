<template>
  <div>
    <button @click="change(now - 1)">Prev</button>
    <button @click="change(now + 1)">Next</button>
    <div class="card-slider">
      <transition-group class="card-slider-items" name="fade">
        <div
          class="card-slider-item"
          v-for="(items, index) in showImages"
          :key="index"
        >
          <img :src="items.src" alt="" />
        </div>
      </transition-group>
    </div>
    <!-- <transition-group
      tag="div"
      :name="transitionName"
      class="box"
      :style="listLength()"
    >
      <div
        v-for="(items, index) in item"
        :key="index"
        class="page"
        :style="listPosition()"
      >
        <img :src="items" alt="" />
        <img
          :src="
            item[
              imgindex == item.length - 1
                ? 0
                : imgindex < 0
                ? item.length - 1
                : index + 1
            ]
          "
          alt=""
        />
      </div>
    </transition-group> -->
  </div>
</template>
<script>
export default {
  data() {
    return {
      now: 0,
      transitionName: "left-in",
      item: [
        "https://images.pexels.com/photos/2583852/pexels-photo-2583852.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        "https://images.pexels.com/photos/2440061/pexels-photo-2440061.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        "https://images.pexels.com/photos/3571576/pexels-photo-3571576.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        "https://images.pexels.com/photos/1067333/pexels-photo-1067333.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        "https://images.pexels.com/photos/1598073/pexels-photo-1598073.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
      ],
    };
  },
  computed: {
    allImages() {
      // 5 + 4
      const ary = [];
      const total = this.item.length;
      let count;
      if (total > 0) {
        while (ary.length < 5 + 4) {
          count = Math.floor(ary.length / total);
          for (let i = 0; i < total; i++) {
            ary.push({
              id: count,
              src: this.item[i],
            });
          }
        }
      }
      return ary;
    },
    showImages() {
      const start = this.now - 4;
      return this.allImages.slice(start).concat(this.allImages.slice(0, start));
    },
  },
  mounted() {
    this.test();
  },
  methods: {
    test() {
      const start = this.now - 4;
      console.log(this.allImages.slice(start), this.allImages.slice(0, start));
      // return this.allImages.slice(start).concat(this.allImages.slice(0, start));
    },
    change(index) {
      const limit = this.allImages.length - 1;
      this.now = index < 0 ? limit : index > limit ? 0 : index;
      // }
    },
  },
};
</script>
<style lang="scss" scoped>
.card-slider {
  display: flex;
  width: 100%;
  overflow: hidden;
  .card-slider-items {
    display: flex;
    width: 100%;
    margin-left: calc(-1 * 25% * 6);
    .card-slider-item {
      flex: calc(80% - 20px) 0 0;
      margin: 10px;
      img {
        width: 100%;
        height: 600px;
      }
    }
  }
  // .card-slider-items {
  //   display: flex;
  //   width: 100%;
  //   margin-left: calc(-1 * 25% * 2.5);
  //   .card-slider-item {
  //     flex: calc(25% - 20px) 0 0;
  //     margin: 10px;
  //     img {
  //       width: 100%;
  //     }
  //   }
  // }
}
</style>