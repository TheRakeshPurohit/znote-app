# 🎨 SVG Logo Studio

This example demonstrates how to render a **logo** using SVG in Znote.

## 🛠 Features:
- ✔ **Run an HTML block** to display the SVG logo.
- ✔ **Use the Color Picker** (right-click on selected text) to customize colors.
- ✔ **Show mouse position** for precise point placement when editing the SVG.


## 🎨 Ubuntu Logo in SVG

```html hide;
<svg xmlns="http://www.w3.org/2000/svg" viewBox="-70 -70 140 140">
  <!-- 🔹 Define reusable shapes -->
  <defs>
    <!-- Main segment of the Ubuntu logo -->
    <path id="segment" d="M 23,-20 A32,32 0,0,0 -23,-20 L -40,-30 A42,42 0,0,1 -14,-47 A17,17 0,0,0 14,-47 A42,42 0,0,1 40,-30 Z"/>
    
    <!-- Small circles in the logo -->
    <circle id="circle" cx="0" cy="-57" r="12"/>
  </defs>

  <!-- 🔸 Shadow Effect -->
  <g transform="translate(5,5)" opacity="0.125">
    <use xlink:href="#circle" transform="rotate(30)"/>
    <use xlink:href="#circle" transform="rotate(150)"/>
    <use xlink:href="#segment" transform="rotate(30)"/>
    <use xlink:href="#circle" transform="rotate(-90)"/>
    <use xlink:href="#segment" transform="rotate(150)"/>
    <use xlink:href="#segment" transform="rotate(-90)"/>
  </g>

  <!-- 🔴 Main Ubuntu Logo Elements -->
  <use xlink:href="#circle" fill="#d00" transform="rotate(30)"/>
  <use xlink:href="#segment" fill="#f40" transform="rotate(30)"/>
  <use xlink:href="#circle" fill="#f80" transform="rotate(150)"/>
  <use xlink:href="#segment" fill="#d00" transform="rotate(150)"/>
  <use xlink:href="#circle" fill="#f40" transform="rotate(-90)"/>
  <use xlink:href="#segment" fill="#f80" transform="rotate(-90)"/>
</svg>
```

---

## 🔧 Customization
You can modify colors using the **Color Picker**:

- `#d00` → **Red**
- `#f40` → **Orange**
- `#f80` → **Light Orange**

📍 To adjust **circle positions**, change the `transform="rotate(deg)"` values.
