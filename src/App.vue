<script setup lang="ts">
import ScrollSlide from './components/ScrollSlide.vue'
</script>

<template>
  <div class="example">
    <h1>Vue 3 Scroll Slides</h1>

    <h2>Independent Templates</h2>
    <ScrollSlide direction="horizontal" :itemGap="15" :itemCount="15"
      style="width: 100%; overflow-x: auto; border: 1px solid #999999; margin-bottom: 40px;" :scale-start-percent="0.95"
      :translate-factor="50">
      <template #item-0>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #E91E63; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🌸 花园 #1
        </div>
      </template>

      <template #item-1>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #9C27B0; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🏙️ 城市 #2
        </div>
      </template>

      <template #item-2>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #673AB7; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          ✨ 极光 #3
        </div>
      </template>

      <template #item-3>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #3F51B5; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🌊 瀑布 #4
        </div>
      </template>

      <template #item-4>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #2196F3; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🌊 湖泊 #5
        </div>
      </template>

      <template #item-5>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #03A9F4; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🏝️ 岛屿 #6
        </div>
      </template>

      <template #item-6>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #00BCD4; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          ❄️ 冰川 #7
        </div>
      </template>

      <template #item-7>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #009688; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🌿 热带雨林 #8
        </div>
      </template>

      <template #item-8>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #4CAF50; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🏔️ 山川 #9
        </div>
      </template>

      <template #item-9>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #8BC34A; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🌲 森林 #10
        </div>
      </template>

      <template #item-10>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #CDDC39; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: black;">
          🌾 草原 #11
        </div>
      </template>

      <template #item-11>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #FFEB3B; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: black;">
          🌞 阳光 #12
        </div>
      </template>

      <template #item-12>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #FFC107; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: black;">
          🏜️ 沙漠 #13
        </div>
      </template>

      <template #item-13>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #FF9800; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: black;">
          🍂 秋叶 #14
        </div>
      </template>

      <template #item-14>
        <div
          style="width: 200px; height: 120px; margin-right: 9px; background-color: #FF5722; border-radius: 10px; display: flex; justify-content: center; align-items: center; color: white;">
          🌋 火山 #15
        </div>
      </template>
    </ScrollSlide>

    <h2>Vertical</h2>
    <ScrollSlide direction="vertical" :itemGap="9" :itemCount="10"
      style="height: 600px; overflow-y: auto; border: 1px solid #999999;">
      <template #item="{ index }">
        <div style="
            width: 100%;
            height: 100px;
            margin-bottom: 9px;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: #ffffff66;
            box-shadow: 0 2px 10px #0000001a;
            backdrop-filter: blur(10px);
            -webkit-backdrop-filter: blur(10px);
            border-radius: 12px;
            border-radius: 15px;
            display: flex;
            justify-content: center;
            align-items: center;
          ">
          Item {{ index + 1 }}
        </div>
      </template>
    </ScrollSlide>

    <h2>Horizontal</h2>
    <ScrollSlide direction="horizontal" :itemGap="9" :itemCount="15"
      style="width: 100%; overflow-x: auto; border: 1px solid #999999;">
      <template #item="{ index }">
        <div style="
            width: 200px;
            height: 100px;
            background-color: #f0f0f055;
            border-radius: 10px;
            display: flex;
            justify-content: center;
            align-items: center;
          ">
          Item {{ index + 1 }}
        </div>
      </template>
    </ScrollSlide>
  </div>
</template>

<style scoped>
.example {
  padding: 20px;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
