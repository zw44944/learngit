<!-- 首页困境树洞困境碎片导航 -->
<template>
  <div class="dilemma">
    <div class="row">
      <div class="column-left">
        <img :src="require('../../assets/images/list-1.jpg')" alt="" />
      </div>
      <div class="column-right">
        <article class="describe">
          <header class="header">
            <h2 class="title">困境树洞</h2>
            <span class="info">Dilemma Tree Hole</span>
          </header>
          <div class="middle">
            <p class="English-dec">
              Keep your face to the sunshine and you cannot see the shadow.
            </p>
            <p class="English-dec">It's what sunflowers do.</p>
            <p class="dec">每天早上醒来把你的脸朝向太阳，</p>
            <p class="dec">你将永远不怕黑暗阴影,</p>
            <p class="dec">
              像向日葵一样永远面对阳光好不退缩的勇气露出灿烂的笑容。
            </p>
          </div>
          <router-link :to="{ name: 'tree' }">
            <div class="bfc">
              <button class="btn">进入</button>
            </div>
          </router-link>
        </article>
      </div>
    </div>
    <div class="row">
      <div class="column-left" style="order: 2">
        <img :src="require('../../assets/images/list-2.png')" alt="" />
      </div>
      <div class="column-right" style="order: 1; text-align: right">
        <article class="describe">
          <header class="header">
            <h2 class="title">困境碎片</h2>
            <span class="info">Dilemma Fragment</span>
          </header>
          <div class="middle">
            <p class="English-dec">
              There is no limit to the goodness of life.
            </p>
            <p class="English-dec">
              It grows more abundant with each new encounter. 
            </p>
            <p class="dec">生命的美好没有界限,</p>
            <p class="dec">每一次相遇都会使这美好变得越发丰富.</p>
          </div>
          <router-link :to="{ name: 'debris' }">
          <div class="bfc">
            <button class="btn">查看详情</button>
          </div>
          </router-link>
        </article>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "dilemma",
};
</script>
<style lang='scss' scoped>
// @import "@/assets/scss/index.scss";
@import "@/assets/scss/mixin.scss";
.dilemma {
  width: 1100px;
  margin: 80px auto;
}
.row {
  display: flex;
  height: 440px;
  margin-bottom: 80px;
}
.column-right {
  width: 40%;
  box-sizing: border-box;
  border: 1px solid rgba(255, 255, 255, 0.5);
  letter-spacing: 0;
  text-indent: 30px;
  padding-right: 30px;
  .describe {
    height: 100%;
    // padding: 0 80px;
    @include flex(space-evenly, strat);
    flex-direction: column;
  }
}
.column-left {
  width: 60%;
  img {
    width: 100%;
    height: 100%;
  }
}
.header {
  .title {
    font-size: 26px;
    margin-bottom: 10px;
  }
  .info {
    display: inline-block;
    color: $lucency-color;
  }
}
.middle {
  .English-dec,
  .dec {
    font-size: 12px;
    line-height: 24px;
    color: $lucency-color;
  }
  .English-dec {
    color: $lucency-color;
    &:nth-child(2) {
      margin-bottom: 10px;
    }
  }
}
</style>