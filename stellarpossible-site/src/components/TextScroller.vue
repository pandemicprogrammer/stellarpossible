<template>
  <div class="content">
    <div class="content__container">
      <div v-if="staticText" class="content__container__static">
        {{ staticText }}
      </div>
      <div class="content__container__divs">
        <div
          class="content__container__divs__item"
          v-for="(item, index) in items"
          :key="index"
          :style="getItemStyle(index)"
        >
          {{ item }}
        </div>
      </div>
    </div>
  </div>
</template>



<script>
export default {
  name: 'TextScroller',
  props: {
    items: {
      type: Array,
      required: true,
    },
    staticText: {
      type: String,
      default: ''
    },
  },
  methods: {
    getItemStyle(index) {
      // For two items, adjust the duration and delay to ensure each is shown in turn.
      const animationDuration = 10; // Example: total duration for both items to be shown.
      const itemDuration = animationDuration / 2; // Each item is shown for half the total duration.
      const delay = index * itemDuration; // Delay for the second item
      
      return {
        animation: `scrollItem ${animationDuration}s linear ${delay}s infinite`,
      };
    },
  },
};
</script>



<style scoped>
.content__container__static {
  /* Styling for the static text */
  color: #ecf0f1; /* Example color */
}
.content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  height: 160px;
  overflow: hidden;
  font-family: 'Lato', sans-serif;
  font-size: 35px;
  line-height: 40px;
  color: #ecf0f1;
}
.content__container {
  font-weight: 600;
  /* overflow: hidden; */
  height: 40px;
  font-family: "M PLUS 1 Code", monospace;
  white-space: nowrap;
}
.content__container::before,
.content__container::after {
  content: '';
  position: absolute;
  top: 0;
  color: #16a085;
  font-size: 42px;
  line-height: 40px;
  animation: opacity 2s infinite;
}
.content__container::before {
  left: 0;
  content: '[';
}
.content__container::after {
  right: 0;
  content: ']';
}
.content__container__divs {
  /* New container for div items */
  margin-top: 0;
  padding-left: 45px;
  text-align: left;
  animation: change 10s infinite;
}
.content__container__divs__item {
  /* Styling for individual div items */
  line-height: 40px;
  margin: 0;
}
@keyframes opacity {
  0%, 100% {opacity: 0;}
  50% {opacity: 1;}
}
@keyframes change {
  0%, 12.66%, 100% {transform: translate3d(0, 0, 0);}
  16.66%, 29.32% {transform: translate3d(0, -25%, 0);}
  33.32%, 45.98% {transform: translate3d(0, -50%, 0);}
  49.98%, 62.64% {transform: translate3d(0, -75%, 0);}
  66.64%, 79.3% {transform: translate3d(0, -50%, 0);}
  83.3%, 95.96% {transform: translate3d(0, -25%, 0);}
}
@keyframes scrollItem {
  0%, 50% { 
    transform: translateY(0); 
  }
  50.1%, 100% { 
    transform: translateY(-100%); 
  }
}
</style>
