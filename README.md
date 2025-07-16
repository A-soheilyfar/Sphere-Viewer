# Sphere-Viewer
this is just a Sphere Viewer library Guide


## 📦 معرفی Sphere Viewer
Sphere Viewer چیست؟
Sphere Viewer (که گاهی با نام‌های مشابه مثل Photo Sphere Viewer, panolens.js, یا Marzipano هم شناخته می‌شود)، یک کتابخانه جاوااسکریپت است که به شما اجازه می‌دهد تصاویر پانورامای کروی (equirectangular) را در صفحات وب نمایش دهید.

یکی از محبوب‌ترین نمونه‌های این دسته، Photo Sphere Viewer است که بر پایه Three.js ساخته شده و قابلیت‌های زیادی دارد.

## ✨ ویژگی‌های کلیدی:
پشتیبانی از تصاویر equirectangular 360°.

چرخش با موس یا تاچ.

زوم کردن.

افزودن نقاط داغ (Hotspots).

حالت VR با WebXR.

پشتیبانی از افزونه‌ها و پلاگین‌ها.

استفاده آسان با Vue، React یا Vanilla JS.




## 🛠️ نصب در Vue.js
1. ## نصب با npm:
   ```bash

   npm install @photo-sphere-viewer/core three
   npm install @photo-sphere-viewer/markers-plugin        # اگر نیاز به پلاگین دارید
   npm install @photo-sphere-viewer/virtual-tour-plugin

   ```

استفاده از نسخه CDN هم ممکن است، اما در پروژه Vue پیشنهاد می‌شود از پک‌های npm استفاده شود 


## 🧩 ۲. راه‌اندازی اولیه در Vue 3

```vue
<template>
  <div ref="container" style="width:100%; height:500px;"></div>
</template>

<script setup>
import { onMounted, ref, onBeforeUnmount } from 'vue'
import { Viewer } from '@photo-sphere-viewer/core'
import { MarkersPlugin } from '@photo-sphere-viewer/markers-plugin'
import '@photo-sphere-viewer/markers-plugin/index.css'
import 'photo-sphere-viewer/styles/photo-sphere-viewer.css'

const container = ref(null)
let viewer

onMounted(() => {
  viewer = new Viewer({
    container: container.value,
    panorama: 'path/to/panorama.jpg',
    defaultYaw: '0deg',
    plugins: [
      [MarkersPlugin, {
        markers: [
          {
            id: 'm-1',
            position: { yaw: '10deg', pitch: '0deg' },
            image: 'pin.png',
            width: 32,
            height: 32,
            tooltip: 'Marker 1',
          },
        ],
      }],
    ],
    navbar: ['zoom', 'fullscreen', 'caption'],
    caption: 'نمای 360 درجه',
    minFov: 30,
    maxFov: 90,
  })
})

onBeforeUnmount(() => {
  viewer.destroy()
})
</script>

```

وارد کردن CSS و پلاگین‌ها ضروری است .

Viewer از پکیج @photo-sphere-viewer/core استفاده می‌کند


🛠️ ۳. تنظیمات کلیدی (options)

   <ul>
      <li>container: عنصر HTML یا selector
</li>
      <li>panorama: مسیر به تصویر equirectangular
</li>
      <li>container: عنصر HTML یا selector
</li>
      <li>plugins: `[PluginClass, config]` آرایه‌ای از 
</li>
   </ul>

   
📌 ۴. اضافه کردن پلاگین‌های مهم
<div dir="rtl">
   <ul>
      <li>MarkersPlugin: برای نشانگرهای تعاملی
</li>
      <li>VirtualTourPlugin: برای ساخت تور مجازی چندتصویری:
</li>
      </ul>
</div>

```js
import { VirtualTourPlugin } from '@photo-sphere-viewer/virtual-tour-plugin'
viewer = new Viewer({
  /* ... */,
  plugins: [
    VirtualTourPlugin.withConfig({
      nodes: [
        {
          id: 'pano1',
          panorama: 'pano1.jpg',
          links: [{ yaw: '180deg', pitch: '0deg', nodeId: 'pano2' }],
        },
        {
          id: 'pano2',
          panorama: 'pano2.jpg',
          links: [{ yaw: '0deg', pitch: '0deg', nodeId: 'pano1' }],
        },
      ],
      startNodeId: 'pano1',
    }),
  ],
})

```
🔧 ۵. پیاده‌سازی عملی در Vue 3
<ul>
   <li>دیالوگ کامل برای راه‌اندازی اولیه
</li>
   <li>نصب پلاگین نشانگر و تور مجازی
</li>
   <li>تنظیم navbar و caption
</li>
   <li>مدیریت lifecycle (mount / destroy)</li>
</ul>



