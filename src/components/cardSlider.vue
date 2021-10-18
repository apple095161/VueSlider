<template>
  <div>
    <button @click="change(now - 1)">pre</button>
    <button @click="change(now + 1)">next</button>
    <div class="card-slider">
      <ul>
        <transition-group class="card-slider-items" name="flip-list">
          <li v-for="img in showImages" :key="img.id" class="card-slider-item">
            <img :src="img.src" alt="" />
          </li>
        </transition-group>
      </ul>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      now: 0,
      imges: [
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
        {
          id: 4,
          src: "https://images.pexels.com/photos/1067333/pexels-photo-1067333.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        },
        {
          id: 5,
          src: "https://images.pexels.com/photos/1598073/pexels-photo-1598073.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=480&w=320",
        },
        {
          id: 6,
          src: "https://images.pexels.com/photos/3244513/pexels-photo-3244513.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260",
        },
        {
          id: 7,
          src: "https://images.pexels.com/photos/624015/pexels-photo-624015.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260",
        },
        {
          id: 8,
          src: "https://images.pexels.com/photos/572897/pexels-photo-572897.jpeg?auto=compress&cs=tinysrgb&dpr=2&h=750&w=1260",
        },
        {
          id: 9,
          src: "https://images.pexels.com/photos/9897346/pexels-photo-9897346.jpeg?auto=compress&cs=tinysrgb&dpr=1&w=500",
        },
      ],
    };
  },
  computed: {
    allImages() {
      const ary = [];
      const total = this.imges.length;
      let count;

      if (total > 0) {
        while (ary.length < this.imges.length + 4) {
          count = Math.floor(ary.length / total);
          for (let i = 0; i < total; i++) {
            ary.push({
              id: count + "-" + this.imges[i].id,
              src: this.imges[i].src,
            });
          }
        }
      }
      return ary;
    },
    showImages() {
      const start = this.now;
      return this.allImages.slice(start).concat(this.allImages.slice(0, start));
    },
  },
  methods: {
    change(index) {
      const limit = this.allImages.length - 1;
      this.now = index < 0 ? limit : index > limit ? 0 : index;
    },
  },
};
</script>
<style lang="scss" scoped>
.card-slider {
  max-width: 600px;
  height: 350px;
  margin: 0 auto;
  overflow: hidden;
  ul {
    display: flex;
    padding: 0;
    margin: 0;
    list-style-type: none;
    .card-slider-items {
      display: flex;
      margin-left: -10px;
      li {
        margin: 10px;
        flex: 85% 0 0;
        img {
          width: 100%;
          height: 350px;
        }
      }
    }
  }
}
// .card-slider-item:first-child,
// .card-slider-item:last-child {
//   z-index: -1;
//   visibility: hidden;
// }
// .flip-list-move {
//   transition: transform 0.5s;
// }
</style>