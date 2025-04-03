<script setup lang="ts">
import { ref, reactive, onMounted, computed, watch, onUnmounted } from 'vue';

// Define component props
const props = defineProps({
  direction: {
    type: String,
    default: 'vertical', // 'vertical' or 'horizontal'
    validator: (value: string) => ['vertical', 'horizontal'].includes(value),
  },
  itemCount: {
    type: Number,
    default: 0,
  },
  scaleRatio: {
    type: Number,
    default: 0.7,
  },
  scaleStartPercent: {
    type: Number,
    default: 0.8,
  },
  translateFactor: {
    type: Number,
    default: 100,
  },
  allowScrollToFirst: {
    type: Boolean,
    default: false,
  },
  // Updating prop name to be clearer
  spacerEnabled: {
    type: Boolean,
    default: false,
  },
});

// Configure slider container and items
const sliderRef = ref<HTMLElement | null>(null);
const items = ref<HTMLElement[]>([]);
const itemStates = reactive<{
  [key: number]: {
    scale: number,
    translate: number,
    opacity: number,
  }
}>({});

// Calculate style-related values
const isVertical = computed(() => props.direction === 'vertical');
const transformProperty = computed(() => isVertical.value ? 'translateY' : 'translateX');

const getPercent = (value: number, total: number) => {
  return Math.min(Math.max(value / total, 0), 1);
};

const ease = (t: number) => {
  return t * t * (3 - 2 * t); // Ease-in-out function
};

// Generate index array for rendering items
const itemIndices = computed(() => Array.from({ length: props.itemCount }, (_, i) => i));

// Handle scroll event
const handleScroll = () => {
  if (!sliderRef.value) return;

  const container = sliderRef.value;
  const viewportSize = container[isVertical.value ? 'clientHeight' : 'clientWidth'];

  items.value.forEach((item, index) => {
    const rect = item.getBoundingClientRect();
    // Item's top or left position on the page
    const itemPos = isVertical.value ? rect.top : rect.left;
    const containerRect = container.getBoundingClientRect();
    // Item's top or left position relative to container
    const relativePos = itemPos - (isVertical.value ? containerRect.top : containerRect.left);

    // Calculate the ratio of visible portion in viewport
    const visibleRatio = Math.min(
      Math.max(0, (viewportSize - relativePos) / viewportSize),
      1
    );

    const transformPercentRaw = getPercent((1 - visibleRatio) - props.scaleStartPercent, 1 - props.scaleStartPercent);

    const transformPercent = ease(transformPercentRaw);

    const scale = 1 + (props.scaleRatio - 1) * transformPercent; // Scale ratio
    const translate = transformPercent * props.translateFactor; // Adjust floating effect

    // Opacity changes from 1 to 0 between 40% and 60%
    let opacity: number;
    const clampedTransformPercent = Math.min(Math.max(transformPercent || 0, 0), 1);
    if (clampedTransformPercent > 0.6) {
      opacity = 0;
    } else if (clampedTransformPercent < 0.4) {
      opacity = 1;
    } else {
      opacity = ((0.6 - clampedTransformPercent) / 0.2);
    }

    // Update state
    itemStates[index] = {
      scale,
      translate,
      opacity,
    };
  });
};

// Reinitialize item list and states
const initializeItems = () => {
  if (sliderRef.value) {
    items.value = Array.from(sliderRef.value.querySelectorAll('.slider-item'));

    // Initialize states for all items
    itemIndices.value.forEach(index => {
      if (!itemStates[index]) {
        itemStates[index] = {
          scale: 1,
          translate: 0,
          opacity: 1,
        };
      }
    });

    // Remove states for items that no longer exist
    Object.keys(itemStates).forEach(key => {
      const index = Number(key);
      if (index >= props.itemCount) {
        delete itemStates[index];
      }
    });

    // Trigger initial calculation
    handleScroll();
  }
};

// Watch for changes in item count
watch(() => props.itemCount, (_newCount, _oldCount) => {
  // Use setTimeout to ensure DOM has updated
  setTimeout(() => {
    initializeItems();
  }, 0);
}, { immediate: false });

// Auto-calculate spacer size based on viewport, minus the first item height
const spacerSize = computed(() => {
  if (!sliderRef.value) return 0;

  const viewportSize = sliderRef.value[isVertical.value ? 'clientHeight' : 'clientWidth'];

  // Get the first item's size if available
  let firstItemSize = 0;
  if (items.value.length > 0) {
    const firstItem = items.value[0];
    if (firstItem) {
      const rect = firstItem.getBoundingClientRect();
      firstItemSize = isVertical.value ? rect.height : rect.width;
    }
  }

  // The spacer should be the size of the viewport minus the first item's size
  // to allow precise positioning of the first element
  return Math.max(0, viewportSize - firstItemSize);
});

// Initialize after component is mounted
onMounted(() => {
  if (sliderRef.value) {
    // Add scroll event listener
    sliderRef.value.addEventListener('scroll', handleScroll);

    // Add resize event listener
    window.addEventListener('resize', handleScroll);

    // Add touch event listener for mobile devices
    sliderRef.value.addEventListener('touchmove', handleScroll, { passive: true });

    // Initialize items
    initializeItems();
  }
});

// Clean up event listeners when component is unmounted
onUnmounted(() => {
  if (sliderRef.value) {
    sliderRef.value.removeEventListener('scroll', handleScroll);
    sliderRef.value.removeEventListener('touchmove', handleScroll);
  }
  window.removeEventListener('resize', handleScroll);
});
</script>

<template>
  <div class="slider" ref="sliderRef" :class="{ 'horizontal': !isVertical }">
    <!-- Add a spacer element at the beginning to allow scrolling with first item at the top/left -->
    <div v-if="spacerEnabled" class="slider-spacer" :style="isVertical
      ? { height: `${spacerSize}px`, minHeight: `${spacerSize}px` }
      : { width: `${spacerSize}px`, minWidth: `${spacerSize}px`, display: 'inline-block' }">
    </div>

    <div v-for="index in itemIndices" :key="index" class="slider-item" :style="{
      zIndex: itemIndices.length - index,
    }">
      <div class="slider-slot" :style="{
        transform: `${transformProperty}(${-itemStates[index]?.translate || 0}%) scale(${itemStates[index]?.scale || 1})`,
        opacity: itemStates[index]?.opacity,
      }">
        <!-- Try to use index-specific slot, fallback to generic item slot if not exist -->
        <slot :name="`item-${index}`" :index="index">
          <slot name="item" :index="index"></slot>
        </slot>
      </div>
    </div>

    <!-- Remove the end spacer as we're using the beginning spacer now -->
  </div>
</template>

<style scoped>
.slider {
  position: relative;
  width: 100%;
  height: 100%;
  overflow-y: auto;
  overflow-x: hidden;
  box-sizing: border-box;
}

.slider.horizontal {
  overflow-x: auto;
  overflow-y: hidden;
  white-space: nowrap;
}

.slider-item {
  position: relative;
}

.slider-item .slider-slot {
  position: relative;
  transition: transform 0.04s;
}

.horizontal .slider-item {
  display: inline-block;
  vertical-align: middle;
  transform-origin: center right;
}

.slider-spacer {
  pointer-events: none;
}
</style>
