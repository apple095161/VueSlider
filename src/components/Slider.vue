<template>
  <div>
    <button @click="change(now - 1)">Prev</button>
    <button @click="change(now + 1)">Next</button>
    <div
      class="card-slider"
      @dragstart="startDrag(item, $event)"
      @drop="onDrop($event, 1)"
      @dragover="dragover"
      @dragend="dragEnd"
      @touchstart="touchstart"
      @touchend="touchend"
    >
      <transition-group class="card-slider-items" name="flip-list">
        <div
          class="card-slider-item"
          v-for="items in showImages"
          :key="items.id"
        >
          <img :src="items.src" alt="" @click="imgClick(items)" />
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
      dpStart: 0,
      thStart: 0,
      transitionName: "left-in",
      item: [
        {
          id: 1,
          src: "https://images.pexels.com/photos/2583852/pexels-photo-2583852.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        },
        {
          id: 2,
          src: "https://images.pexels.com/photos/2440061/pexels-photo-2440061.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        },
        {
          id: 3,
          src: "https://images.pexels.com/photos/3571576/pexels-photo-3571576.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        },
        // {
        //   id: 4,
        //   src: "https://images.pexels.com/photos/1067333/pexels-photo-1067333.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        // },
        // {
        //   id: 5,
        //   src: "https://images.pexels.com/photos/1598073/pexels-photo-1598073.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        // },
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
        while (ary.length < 3 + 4) {
          count = Math.floor(ary.length / total);
          for (let i = 0; i < total; i++) {
            ary.push({
              id: count + "-" + this.item[i].id,
              src: this.item[i].src,
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
    onDrop() {
      // if (ev.clientX > 150) {
      //   ev.target.style.transform = `translateX(${ev.clientX}px)`;
      // }
    },
    dragover() {
      // const el = document.querySelector(".card-slider .card-slider-items");
      // console.log(ev);
      // if (ev.clientX < 1920 / 2) {
      //   el.style.transform = `translateX(${ev.clientX}px)`;
      // } else {
      //   el.style.transform = `translateX(-${this.dpStart - ev.clientX}px)`;
      // }
    },
    startDrag(s, ev) {
      this.dpStart = ev.clientX;
    },
    dragEnd(ev) {
      // const el = document.querySelector(".card-slider .card-slider-items");
      if (ev.clientX - this.dpStart > 50) {
        this.now--;
        if (this.now < 0) {
          this.now = 9;
        }
      } else if (ev.clientX - this.dpStart < -50) {
        this.now++;
        if (this.now > this.showImages.length - 1) {
          this.now = 0;
        }
      }
    },
    imgClick() {
      // console.log(item);
    },
    test() {
      // const start = this.now - 4;
      // console.log(this.allImages.slice(start), this.allImages.slice(0, start));
      // return this.allImages.slice(start).concat(this.allImages.slice(0, start));
    },
    touchstart(ev) {
      this.thStart = ev.touches[0].clientX;
    },
    touchend(ev) {
      let thMOve = ev.changedTouches[0].clientX;
      if (thMOve - this.thStart > 50) {
        this.now--;
        if (this.now < 0) {
          this.now = 9;
        }
      } else if (thMOve - this.thStart < -50) {
        this.now++;
        if (this.now > this.showImages.length - 1) {
          this.now = 0;
        }
      }
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
  margin: 0 auto;
  max-width: 600px;
  .card-slider-items {
    display: flex;
    width: 100%;
    margin-left: calc(-1 * 25% * 6);
    .card-slider-item {
      flex: calc(80% - 20px) 0 0;
      margin: 10px;
      img {
        width: 100%;
        height: 500px;
      }
      &:first-child {
        z-index: -1;
        visibility: hidden;
      }
      &:last-child {
        z-index: -1;
        visibility: hidden;
      }
    }
  }
}
.card-slider-item:first-child,
.card-slider-item:last-child {
  z-index: -1;
  visibility: hidden;
}
.flip-list-move {
  transition: transform .5s;
}
</style>