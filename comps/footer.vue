<template>
  <footer id="footer" class="flex w100">
    <div class="middle flexc">
      <span>Copyright (c) 2022-2022 <b><a target="_blank" :href="'https://github.com/'+user">even-day</a> | {{ hostName }}</b></span>
      <span class="flex"><a class="rss" target="_blank" href="/sitemap.xml" title="rss">RSS <svg-icon name="rss"/></a>| Powered By <a class="nuxt" href="https://nuxtjs.org/" target="_blank">Nuxtjs</a> 已运行<span id='days'></span>天</span>
    </div>
  </footer>
</template>

<script>
import {inBrowser} from "~/utils/utils";
import config from "@/config";

if (process.client) {
var s1 = '2022-03-22';//设置为你的建站时间
s1 = new Date(s1.replace(/-/g, "/"));
var s2 = new Date();
var days = s2.getTime() - s1.getTime();
var number_of_days = parseInt(days / (1000 * 60 * 60 * 24));
document.getElementById("days").innerHTML = number_of_days;
}

export default {
  name: "the-footer",
  data() {
    return {
      user: config.githubName,
      hostName: inBrowser ? location.hostname : ''
    }
  }
}
</script>

<style lang="scss">
@import "assets/style/var";
#footer{
  height: $footer-height;
  .middle{
    font-size: 13px;
    color: #7c7c7c;
    margin: auto;
    transition: $common-transition;
    b{
      transition: $common-transition;
    }
    span:last-of-type{
      margin: 6px 0;
    }
  }
  &:hover{
    .middle{
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
