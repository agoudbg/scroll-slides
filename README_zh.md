# scroll-slides

[English](./README.md) | 简体中文

一个流畅且可自定义的基于滚动的幻灯片动画组件，适用于 Vue 3。通过动态缩放、平移和遮挡效果创建引人入胜的滚动体验。

![npm version](https://img.shields.io/npm/v/scroll-slides.svg)
![license](https://img.shields.io/npm/l/scroll-slides.svg)

## ✨ 特性

- 🎯 **流畅的滚动动画** - 随着滚动优雅地缩放和平移元素
- 📱 **方向支持** - 支持垂直和水平滚动模式
- 🎨 **高度可自定义** - 微调动画参数以匹配您的设计
- 🔄 **动态项目管理** - 动态添加或删除项目
- 📐 **灵活的模板** - 使用通用或单独的插槽模板
- 🚀 **性能优化** - 高效的事件处理和 DOM 更新
- 💅 **TypeScript 支持** - 包含完整的类型定义
- 🎭 **遮挡效果** - 可选的下层项目裁剪以增强深度感

## 📦 安装

```bash
npm install scroll-slides
```

```bash
yarn add scroll-slides
```

```bash
pnpm add scroll-slides
```

## 🚀 快速开始

### 基础用法

```vue
<script setup>
import { ScrollSlide } from 'scroll-slides';
</script>

<template>
  <ScrollSlide
    direction="vertical"
    :item-count="10"
    style="height: 600px; overflow-y: auto;"
  >
    <template #item="{ index }">
      <div class="slide-item">
        幻灯片 {{ index + 1 }}
      </div>
    </template>
  </ScrollSlide>
</template>

<style scoped>
.slide-item {
  width: 100%;
  height: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border-radius: 15px;
  color: white;
  margin-bottom: 10px;
}
</style>
```

### 水平滚动

```vue
<template>
  <ScrollSlide
    direction="horizontal"
    :item-count="15"
    :scale-start-percent="0.95"
    :translate-factor="50"
    :spacer-enabled="true"
    style="width: 100%; height: 200px; overflow-x: auto;"
  >
    <template #item="{ index }">
      <div class="horizontal-item">
        项目 {{ index + 1 }}
      </div>
    </template>
  </ScrollSlide>
</template>

<style scoped>
.horizontal-item {
  width: 200px;
  height: 120px;
  margin-right: 15px;
  background: #4CAF50;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
}
</style>
```

### 独立模板

您可以使用索引插槽为每个项目定义独特的内容：

```vue
<template>
  <ScrollSlide direction="vertical" :item-count="3">
    <template #item-0>
      <div class="custom-item">🌸 第一项</div>
    </template>
    
    <template #item-1>
      <div class="custom-item">🎨 第二项</div>
    </template>
    
    <template #item-2>
      <div class="custom-item">🚀 第三项</div>
    </template>
  </ScrollSlide>
</template>
```

## 📖 API 参考

### Props 属性

| 属性 | 类型 | 默认值 | 描述 |
|------|------|---------|-------------|
| `direction` | `'vertical' \| 'horizontal'` | `'vertical'` | 滚动方向 |
| `itemCount` | `number` | `0` | 列表中的项目总数 |
| `scaleRatio` | `number` | `0.7` | 项目滑出时的最终缩放比例 (0-1) |
| `scaleStartPercent` | `number` | `0.8` | 开始缩放的阈值百分比 (0-1) |
| `translateFactor` | `number` | `100` | 滑出期间的位移偏移调整 |
| `spacerEnabled` | `boolean` | `false` | 在开始处添加占位符以允许第一项滚出 |
| `occludeLowerItems` | `boolean` | `false` | 应用裁剪路径以防止视觉重叠 |

### 插槽

#### 默认项目插槽

当没有定义特定项目插槽时使用：

```vue
<template #item="{ index }">
  <!-- 您的内容 -->
  <!-- index: number - 当前项目的从零开始的索引 -->
</template>
```

#### 索引项目插槽

为特定项目定义独特的内容：

```vue
<template #item-0>
  <!-- 第一项的内容 -->
</template>

<template #item-1>
  <!-- 第二项的内容 -->
</template>
```

**注意：** 索引插槽优先于通用的 `#item` 插槽。

#### 占位符插槽

自定义占位符元素（当 `spacerEnabled` 为 `true` 时）：

```vue
<template #spacer="{ size }">
  <!-- size: number - 占位符的计算大小（像素） -->
  <div>自定义占位符内容</div>
</template>
```

## 🎨 自定义示例

### 微妙动画

```vue
<ScrollSlide
  :scale-ratio="0.9"
  :scale-start-percent="0.95"
  :translate-factor="20"
  :item-count="10"
>
  <template #item="{ index }">
    <!-- 您的内容 -->
  </template>
</ScrollSlide>
```

### 戏剧效果

```vue
<ScrollSlide
  :scale-ratio="0.5"
  :scale-start-percent="0.7"
  :translate-factor="150"
  :occlude-lower-items="true"
  :item-count="10"
>
  <template #item="{ index }">
    <!-- 您的内容 -->
  </template>
</ScrollSlide>
```

### 水平卡片轮播

```vue
<ScrollSlide
  direction="horizontal"
  :item-count="20"
  :scale-ratio="0.85"
  :scale-start-percent="0.9"
  :translate-factor="30"
  :spacer-enabled="true"
  style="width: 100%; height: 250px; overflow-x: auto;"
>
  <template #item="{ index }">
    <div class="card">
      卡片 {{ index + 1 }}
    </div>
  </template>
</ScrollSlide>
```

## 🔧 高级用法

### 动态项目数量

```vue
<script setup>
import { ref } from 'vue';
import { ScrollSlide } from 'scroll-slides';

const items = ref([1, 2, 3, 4, 5]);

const addItem = () => {
  items.value.push(items.value.length + 1);
};

const removeItem = () => {
  items.value.pop();
};
</script>

<template>
  <div>
    <button @click="addItem">添加项目</button>
    <button @click="removeItem">删除项目</button>
    
    <ScrollSlide :item-count="items.length">
      <template #item="{ index }">
        <div>项目 {{ items[index] }}</div>
      </template>
    </ScrollSlide>
  </div>
</template>
```

### 响应式配置

```vue
<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue';
import { ScrollSlide } from 'scroll-slides';

const windowWidth = ref(window.innerWidth);

const direction = computed(() => 
  windowWidth.value < 768 ? 'vertical' : 'horizontal'
);

const updateWidth = () => {
  windowWidth.value = window.innerWidth;
};

onMounted(() => window.addEventListener('resize', updateWidth));
onUnmounted(() => window.removeEventListener('resize', updateWidth));
</script>

<template>
  <ScrollSlide
    :direction="direction"
    :item-count="10"
    :style="direction === 'vertical' 
      ? 'height: 500px; overflow-y: auto;' 
      : 'width: 100%; overflow-x: auto;'"
  >
    <template #item="{ index }">
      <!-- 响应式内容 -->
    </template>
  </ScrollSlide>
</template>
```

## 💡 技巧与最佳实践

1. **容器样式**：始终在 ScrollSlide 容器上设置明确的尺寸和溢出属性：
   ```vue
   <ScrollSlide style="height: 600px; overflow-y: auto;">
   ```

2. **项目间距**：将边距添加到项目内容，而不是插槽包装器：
   ```css
   .my-item {
     margin-bottom: 10px; /* 垂直方向 */
     margin-right: 10px;  /* 水平方向 */
   }
   ```

3. **性能**：对于大列表，考虑结合虚拟滚动技术使用 scroll-slides。

4. **Z-Index**：项目自动按逆序设置 z-index（第一项在顶部）。请相应地规划您的设计。

5. **占位符用法**：当您希望第一项能够滚动到视口中心/顶部时，启用 `spacerEnabled`。

## 🛠️ 开发

```bash
# 克隆仓库
git clone https://github.com/agoudbg/scroll-slides.git

# 安装依赖
pnpm install

# 运行开发服务器
pnpm dev

# 构建库
pnpm build

# 构建演示
pnpm build:demo
```

## 📄 许可证

MIT 许可证 - 详见 [LICENSE](LICENSE) 文件

## 🤝 贡献

欢迎贡献、提出问题和功能请求！请随时查看 [issues 页面](https://github.com/agoudbg/scroll-slides/issues)。

## 👤 作者

**agoudbg**
- GitHub: [@agoudbg](https://github.com/agoudbg)
- Email: agoudbg@gmail.com

## 🌟 支持我们

如果这个项目对您有帮助，请给一个 ⭐️！

---

使用 Vue 3 和 TypeScript 用 ❤️ 制作
