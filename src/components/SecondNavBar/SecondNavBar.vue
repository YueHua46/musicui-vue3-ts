<template>
  <div class="sNavBarContainer">
    <div
      v-for="(item, index) in hotTagData"
      :key="index"
      :class="currentTagData.name === item.name ? 'active' : ''"
      class="sNavBarItem"
      @click="clicksNavBarItem(Number(index))"
    >
      <span :class="currentTagData.name === item.name ? 'activeFont' : ''">{{
        item.name
      }}</span>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, watch,watchEffect } from "vue";
type HotTagDataType = {area?:number,name?:string}

const props = withDefaults(defineProps<{
  hotTagData:HotTagDataType[],
  currentTagData?:HotTagDataType
}>(),{
  currentTagData: () => ({})
})

watch(props.hotTagData, (value, oldValue, onCleanup) => {
  console.log('props.hotTagData',props.hotTagData);
  console.log('value',value);
});

watchEffect(() => {
  console.log('props.hotTagData',props.hotTagData);
  console.log('props.currentTagData',props.currentTagData);
});

const activeIndex = ref(-1);

const emits = defineEmits(["clicksNavBarItem"]);

const clicksNavBarItem = (index: number) => {
  if (activeIndex.value == index) {
    return;
  }
  activeIndex.value = index;
  emits("clicksNavBarItem", index);
};
</script>

<style lang="less" scoped>
.sNavBarContainer {
  width: 100vmin;
  height: 3.95vmin;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap;
  border-radius: 20px;

  .sNavBarItem {
    border-radius: 2vmin;
    box-shadow: 0 0 2px 2px rgb(255, 255, 255);
    margin: 0 0.55vmin;
    padding: 0 1vmin;
    color: #555;
    cursor: pointer;

    span {
      font-size: 2.233vmin;
    }
  }
}

.active {
  background-color: #f5c6c6;
}

.activeFont {
  color: #ec4141;
}
</style>