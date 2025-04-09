<script setup lang="ts">
import ScrollSlide from './components/ScrollSlide.vue'
import { ref } from 'vue'

const direction = ref('vertical')
const itemGap = ref(9)
const itemCount = ref(10)
const scaleStartPercent = ref(0.85)
const translateFactor = ref(120)
const spacerEnabled = ref(false)
</script>

<template>
  <div class="example">
    <h1>Vue 3 Scroll Slides</h1>

    <h2>Independent Templates</h2>
    <ScrollSlide direction="horizontal" :itemGap="15" :itemCount="15"
      style="width: 100%; overflow-x: auto; border: 1px solid #999999; margin-bottom: 40px;" :scale-start-percent="0.95"
      :translate-factor="50" :spacer-enabled="true">
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
    <div class="settings-panel">
      <div class="setting-item">
        <label>Direction:</label>
        <select v-model="direction">
          <option value="vertical">vertical</option>
          <option value="horizontal">horizontal</option>
        </select>
      </div>
      <div class="setting-item">
        <label>Gap:</label>
        <input type="number" v-model.number="itemGap" min="0" max="50" />
      </div>
      <div class="setting-item">
        <label>Item count:</label>
        <input type="number" v-model.number="itemCount" min="1" max="20" />
      </div>
      <div class="setting-item">
        <label>Scale start percent:</label>
        <input type="number" v-model.number="scaleStartPercent" min="0.5" max="1" step="0.05" />
      </div>
      <div class="setting-item">
        <label>Translate factor:</label>
        <input type="number" v-model.number="translateFactor" min="0" max="100" />
      </div>
      <div class="setting-item">
        <label>Enable leading spacer:</label>
        <input type="checkbox" v-model="spacerEnabled" />
      </div>
    </div>

    <ScrollSlide :direction="direction" :itemGap="itemGap" :itemCount="itemCount"
      :scale-start-percent="scaleStartPercent" :translate-factor="translateFactor" :spacer-enabled="spacerEnabled"
      :style="direction === 'vertical'
        ? 'height: 600px; overflow-y: auto; border: 1px solid #999999;'
        : 'width: 100%; height: 200px; overflow-x: auto; border: 1px solid #999999;'">
      <template #item="{ index }">
        <div :style="{
          width: direction === 'vertical' ? '100%' : '200px',
          height: direction === 'vertical' ? '100px' : '120px',
          marginBottom: direction === 'vertical' ? itemGap + 'px' : '0px',
          marginRight: direction === 'horizontal' ? itemGap + 'px' : '0px',
          display: 'flex',
          justifyContent: 'center',
          alignItems: 'center',
          backgroundColor: '#ffffff66',
          boxShadow: '0 2px 10px #0000001a',
          backdropFilter: 'blur(10px)',
          webkitBackdropFilter: 'blur(10px)',
          borderRadius: '15px',
        }">
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

.settings-panel {
  display: flex;
  flex-wrap: wrap;
  gap: 15px;
  margin-bottom: 20px;
  padding: 15px;
  background-color: #f5f5f5;
  border-radius: 8px;
}

.setting-item {
  display: flex;
  flex-direction: column;
  min-width: 120px;
}

.setting-item label {
  margin-bottom: 5px;
  font-size: 14px;
}

.setting-item input,
.setting-item select {
  padding: 8px;
  border: 1px solid #ddd;
  border-radius: 4px;
}
</style>
