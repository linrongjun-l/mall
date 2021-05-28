<template>
  <div id="tab-control">
    <div class="item-control" v-for="(item, index) in titles"
         :class="{'item-control-active':index == curIndex}"
         @click="itemClick(index)">
      <span>{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "TabControl",
  data(){
    return {
      curIndex: 0,
    }
  },
  props: {
    titles: {
      type: Array,
      default(){
        return []
      }
    }
  },
  methods: {
    itemClick(index){
      this.curIndex = index;
      //把index传给Home组件
      this.$emit("tabClick",index);
    }
  }
}
</script>

<style >
#tab-control{
  display: flex;
  text-align: center;
  font-size: 15px;
  height: 40px;
  line-height: 40px;
  background: #fff;
}

.item-control{
  flex: 1;
}

.item-control-active{
  color:var(--color-high-text);
}

.item-control-active span{
  padding: 5px;
  border-bottom: 2px solid var(--color-high-text);
}
</style>