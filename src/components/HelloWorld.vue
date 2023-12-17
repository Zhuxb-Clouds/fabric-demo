<template>
  <div>
    <canvas ref="canvas" style="border: 1px #000 solid;"></canvas>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { fabric } from 'fabric';

const canvas = ref(null);
const pressure = ref(0.3);

onMounted(() => {
  // 初始化 Fabric.js canvas
  const fabricCanvas = new fabric.Canvas(canvas.value, {
    width: 800,
    height: 600,
    backgroundColor: 'white', // 设置画布背景色.
    isDrawingMode: true,
    enablePointerEvents: true
  });

  // 添加一个简单的矩形到 canvas
  const rect = new fabric.Rect({
    top: 100,
    left: 100,
    width: 200,
    height: 100,
    fill: 'red'
  });

  fabricCanvas.add(rect); // 将矩形添加到 canvas

  // Initialize a brush
  let brush = new fabric.PSBrush(fabricCanvas);
  fabricCanvas.freeDrawingBrush = brush;

  // Set some options...
  brush.width = 10;
  brush.color = "#000";
  brush.disableTouch = true; // disable touch and only use mouse and pen devices
  brush.pressureManager.fallback = pressure.value; 
});
</script>
