<template>
  <div class="discoverContainer">
    <NavBar :navBarData="navBarData" @clickBarItem="clickBarItem"></NavBar>
    <RouterView class="discover"></RouterView>
  </div>
</template>

<script lang="ts" setup>
import NavBar from "@/components/NavBar/NavBar.vue";
import { onMounted, ref } from "vue";
import router from "@/router/router";

const navBarData = ref([
  {
    name: "个性推荐",
    path: "/discover/personrecommend",
  },
  {
    name: "歌单",
    path: "/discover/songlist",
  },
  {
    name: "排行榜",
    path: "/discover/ranking",
  },
  {
    name: "歌手",
    path: "/discover/songer",
  },
]);
onMounted(() => {
  console.log("Mounted");
});
const clickBarItem = (path: any, index: any, indexData: any) => {
  router.push(path);
  // indexData.activeIndex = index;
};
</script>

<style lang="less" scoped>
.discoverContainer {
  padding: 0 !important;
  overflow: hidden;

  .discover {
    overflow: scroll;
    height: calc(100vh - 25.55vmin);
    //height: calc(100vh - 212px);
  }
}
</style>