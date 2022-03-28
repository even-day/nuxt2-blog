<template>
  <footer id="footer" class="flex w100">
    <div class="middle flexc">
      <span>Copyright (c) 2022-2022<b><a target="_blank" :href="'https://github.com/' + user">even-day</a> | {{ hostName }}</b></span>
      <span class="flex"><a class="rss" target="_blank" href="/sitemap.xml" title="rss">RSS <svg-icon name="rss" /></a>| Powered By<a class="nuxt" href="https://nuxtjs.org/" target="_blank">Nuxtjs</a>| 本站已安全运行{{ dnum }}天 {{ hnum }}小时 {{ mnum }}分 {{ snum }}秒</span>
    </div>
  </footer>
</template>

<script>
import { inBrowser } from "~/utils/utils";
import config from "@/config";

export default {
  name: "the-footer",
  data() {
    return {
      user: config.githubName,
      hostName: inBrowser ? location.hostname : "",
      timer: "",
      dnum: 0,
      hnum: 0,
      mnum: 0,
      snum: 0,
    };
  },
  created() {},
  mounted() {
    // setInterval函数中的this指向是window而不是vue , 所以这里需要将this赋值给that , 在setInterval中用that代替this
    let that = this;
    // 每隔1000毫秒就调用一次createTime()
    this.timer = setInterval(function () {
      that.createTime();
    }, 1000);
  },
  // 销毁这个定时任务
  beforeDestroy() {
    clearInterval(this.timer);
  },

  methods: {
    // 这里是计算建站时间的脚本
    createTime() {
      let now = new Date();
      // 页脚建站时间计算脚本
      var grt = new Date("03/22/2022 17:21:13"); //在此处修改你的建站时间，格式：月/日/年 时:分:秒
      now.setTime(now.getTime() + 250);

      let days = (now - grt) / 1000 / 60 / 60 / 24;
      this.dnum = Math.floor(days);
      let hours = (now - grt) / 1000 / 60 / 60 - 24 * this.dnum;
      this.hnum = Math.floor(hours);
      if (String(this.hnum).length == 1) {
        this.hnum = "0" + this.hnum;
      }
      let minutes =
        (now - grt) / 1000 / 60 - 24 * 60 * this.dnum - 60 * this.hnum;
      this.mnum = Math.floor(minutes);
      if (String(this.mnum).length == 1) {
        this.mnum = "0" + this.mnum;
      }
      let seconds =
        (now - grt) / 1000 -
        24 * 60 * 60 * this.dnum -
        60 * 60 * this.hnum -
        60 * this.mnum;
      this.snum = Math.round(seconds);
      if (String(this.snum).length == 1) {
        this.snum = "0" + this.snum;
      }
    },
  },
};
</script>

<style lang="scss">
@import "assets/style/var";
#footer {
  height: $footer-height;
  .middle {
    font-size: 13px;
    color: #7c7c7c;
    margin: auto;
    transition: $common-transition;
    b {
      transition: $common-transition;
    }
    span:last-of-type {
      margin: 6px 0;
    }
  }
  &:hover {
    .middle {
      color: black;
    }
  }
  a {
    color: #1c1c1c;
    transition: $common-transition;
    &:hover {
      color: #2eb1c9;
    }
  }
  .nuxt {
    margin-left: 5px;
    margin-right: 5px;
  }
  .rss {
    display: inline-flex;
    align-items: center;
    margin-right: 5px;
    transition: $common-transition;
    fill: #00a4a4;
    svg {
      width: 16px;
      height: 16px;
      margin-left: 5px;
    }
    &:hover {
      transform: scale(1.1);
      fill: #00c9c9;
    }
  }
}
</style>
