<template>
  <div>
    <div class="box">
      <div class="head">todoList</div>
      <input
        type="text"
        v-model="val"
        @keyup="an"
        class="int"
        placeholder="请输入你的计划"
      />
      <ul class="ull">
        <li
          class="lii"
          v-for="(item, index) in arr"
          :key="index"
          v-show="item.flag == false"
        >
          <span>
            <input type="checkbox" v-model="item.flag" />{{ item.name }}</span
          >
          <button @click="del(index)">删除</button>
        </li>
      </ul>
      <ul class="ull">
        <li
          class="lii"
          v-for="(item, index) in arr"
          :key="index"
          v-show="item.flag == true"
        >
          <span>
            <input type="checkbox" checked v-model="item.flag" />{{
              item.name
            }}</span
          >
          <button @click="del(index)">删除</button>
        </li>
      </ul>
      <div class="font">
        <span>待完成:{{ total.wei }}</span>
        <span>已完成：{{ total.yi }}</span>
      </div>
    </div>
  </div>
</template>
<script setup>
import { reactive, ref, computed } from "vue";
const val = ref("");
const arr = reactive([]);
// 添加
const an = function (e) {
  if (e.keyCode == 13) {
    if (val.value == "") {
      alert("不能为空");
      return false;
    }
    arr.push({
      name: val.value,
      flag: false,
    });
    console.log(arr);
    val.value = "";
  }
};
// 删除
const del = function (index) {
  arr.splice(index, 1);
};
// 计算数量
const total = computed(() => {
  let yi = 0;
  let wei = 0;
    arr.forEach((item) => {
      if (item.flag == true) {
        yi += 1;
      } else if (item.flag == false) {
        wei += 1;
      }
    });
  return { yi, wei };
});
</script>
<style>
.box {
  width: 500px;
  height: 500px;
  border: 2px solid #000;
  margin: 30px auto;
}
.head {
  margin-top: 20px;
  font-weight: 900;
  font-size: 30px;
  text-align: center;
}
.int {
  width: 92%;
  height: 30px;
  /* margin: auto; */
  margin-left: 20px;
  text-indent: 10px;
  margin-top: 20px;
}
.ull {
  width: 100%;
}
.lii {
  margin-top: 10px;
  height: 40px;
  width: 100%;
  /* text-align: center; */
  display: flex;
  justify-content: space-around;
  align-items: center;
  list-style: none;
  /* border: 1px solid #ccc; */
  border-bottom: 1px solid #ccc;
}
.font {
  margin-top: 10px;
  width: 100%;
  height: 40px;
  display: flex;
  justify-content: space-around;
}
</style>