<!-- 选择困境 -->
<template>
  <div class="select-page container">
    <div class="nav-box">
      <ul class="nav-bar" ref="ul">
        <li
          class="nav-item"
          v-for="(item, index) in PageList"
          :key="index"
          @click="routePush(item, $event)"
        >
          {{ item }}
        </li>
      </ul>
      <div ref="line" class="nav-line"></div>
    </div>
    <div class="wrap">
      <header class="header">
        <h2 class="title">亲爱的自己</h2>
        <span class="English">DEAR SELF</span>
      </header>
      <div
        class="content"
        :class="[interspace === 'school' ? 'content-circle' : 'content-rect']"
      >
        <router-link class="box" v-for="(item, index) in randerData" :key="index" :to="{ name: item.name, params: { tag: [item.grandpa, item.father, item.title] } }">
          <div class="kernel">
            <img :src="item.imgurl" alt="" />
            <h4 class="plight-title">{{ item.title }}</h4>
            <span class="plight-dec">{{ item.english }}</span>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "space-select",
  components: {},
  data() {
    return {
      interspace: "",
      currnetPage: "",
      PageList: [],
      randerData: [],
    };
  },
  props: ["selectIdentity"],
  watch: {
    $route: {
      handler(to) {
        this.interspace = to.params.interspace;
        if (this.interspace) {
          this.currnetPage = to.query.name;
          this.init();
          this.$nextTick().then(() => {
            this.lineMove(this.currnetPage);
          });
        }
      },
      deep: true,
      immediate: true,
    },
  },
  //方法集合
  methods: {
    init() {
      let PageList = [];
      this.selectIdentity[this.interspace].forEach((item) => {
        PageList.push(item.title);
        if (item.title === this.currnetPage) {
          this.randerData = item;
        }
      });
      this.PageList = PageList;
      this.randerData = this.randerData.dilemma.map((item) => item);
    },
    routePush(name, event) {
      this.$router.push({ query: { name } });
    },
    lineMove(name) {
      const list = [...this.$refs.ul.querySelectorAll(".nav-item")];
      const Vnode = list.find((item) => {
        return item.innerText === name;
      });
      const width = Vnode.offsetWidth;
      const left = Vnode.offsetLeft;
      this.$refs.line.style.cssText = `left:${left}px;width:${width}px`;
    },
  },
};
</script>
<style lang='scss' scoped>
@import "@/assets/scss/mixin.scss";
.select-page {
  color: $font-color;
}
.nav-box {
  position: relative;
  .nav-bar {
    @include flex(center);
    height: 50px;
    border-bottom: 1px solid #e8e9eb;
    .nav-item {
      margin: 0 50px;
      cursor: pointer;
    }
  }
  .nav-line {
    position: absolute;
    bottom: 0;
    height: 3px;
    width: 100px;
    background-color: #6b63b5;
    transition: all 0.4s;
  }
}
.wrap {
  padding: 50px 0 100px;
  .title {
    font-size: 26px;
    font-weight: 400;
  }
  .English {
    font-size: 12px;
    color: #808080;
    letter-spacing: 0;
  }
}
.content {
  margin-top: 60px;
  @include flex();
}
.router {
  height: 320px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.content .box:hover::before {
  box-shadow: 0 0 30px rgba(51, 51, 51, 0.329);
}

.content .box {
  position: relative;
  width: 322px;
  height: 322px;
  background-size: contain;
  background-repeat: no-repeat;
  // background-color: #6b63b5;
}

.content .kernel {
  position: absolute;
  top: 2px;
  width: 100%;
  z-index: auto;
  text-align: center;
  letter-spacing: 0;
  .plight-title {
    margin-top: 8px;
    font-size: 16px;
    font-weight: 400;
  }
  .plight-dec {
    font-size: 12px;
    color: #999;
  }
}

.content.content-circle .kernel {
  .plight-title {
    margin-top: -8px;
    font-size: 16px;
    font-weight: 400;
  }
  .plight-dec {
    font-size: 12px;
    color: #999;
  }
}

.box::before {
  transition: all 1s;
  cursor: pointer;
}
.box::after {
  cursor: pointer;
}

.content .box::before,
.content .box::after {
  position: absolute;
  content: "";
}
.content-circle .box img {
  width: 100%;
  height: 100%;
}
.content-circle .box::before {
  top: 0%;
  left: 0%;
  right: 0%;
  bottom: 0%;
  border-radius: 50%;
  z-index: 0;
  background-color: #fff;
}
.content-circle .box::after {
  top: 5%;
  left: 5%;
  right: 5%;
  bottom: 5%;
  border-radius: 50%;
  z-index: 0;
  border: 1px solid #fff;
}

.content-rect .box::before {
  top: 15%;
  left: 15%;
  right: 15%;
  bottom: 15%;
  z-index: 0;
  background-color: #fff;
  transform: rotate(-45deg);
}
.content-rect .box::after {
  top: 20%;
  left: 20%;
  right: 20%;
  bottom: 20%;
  z-index: 0;
  border: 1px solid #fff;
  transform: rotate(-45deg);
}
</style>