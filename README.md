# 🎮 GitHub Profile — *Game Mode*

> Bikin profilmu berasa main game: ada **HUD**, **Quest**, **Power‑Ups**, dan **animasi Snake** dari kontribusi.

---

## HUD

![Lives](https://img.shields.io/badge/❤❤❤❤❤-Lives-red)
![Level](https://img.shields.io/badge/Level-06-blue)
![XP](https://img.shields.io/badge/XP-3,250-brightgreen)
![Streak](https://img.shields.io/badge/Streak-🔥%20keep%20going!-orange)

> *Data enthusiast & mobile/web tinkerer — IoT, Realtime, Maps.*

---

## 🗺️ Map (Tech Tree)

![Python](https://img.shields.io/badge/Python-3776AB?logo=python\&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript\&logoColor=black)
![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?logo=typescript\&logoColor=white)
![React](https://img.shields.io/badge/React-20232a?logo=react\&logoColor=61DAFB)
![Next.js](https://img.shields.io/badge/Next.js-000000?logo=next.js\&logoColor=white)
![React%20Native](https://img.shields.io/badge/React_Native-20232a?logo=react\&logoColor=61DAFB)
![MQTT](https://img.shields.io/badge/MQTT-660066?logo=eclipsemosquitto\&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-010101?logo=socketdotio\&logoColor=white)
![Leaflet](https://img.shields.io/badge/Leaflet-199900?logo=leaflet\&logoColor=white)

---

## 🏆 Achievements

* 🛰️ **IoT Rookie** — publish data dummy banjir via MQTT.
* 🗺️ **Cartographer** — realtime map marker dengan Leaflet.
* 🔐 **Guardian** — auth sederhana untuk chat & share lokasi.
* ⚡ **Low‑latency** — Socket.IO event <100ms di jaringan lokal.

> (Semua achievements otomatis “naik level” seiring update proyek.)

---

## 🎯 Quests (to‑do publik)

* [ ] Rilis **demo GIF** untuk tiap repo unggulan.
* [ ] Tambah **unit test** minimal di proyek utama.
* [ ] Deploy **GitHub Pages** mini‑game (lihat di bawah).
* [ ] Tulis **README ringkas** per repo (value + cara jalan).
* [ ] Tambah **topics**: `iot`, `realtime`, `leaflet`, `socket.io`, `react-native`, `nextjs`.

> Centang sambil jalan biar profilmu hidup dan interaktif.

---

## ⚗️ Power‑Ups (Projects)

* **Makassar Flood Monitoring (MQTT + Python + Dashboard)** — *Simulasi IoT banjir*.
  `power: sensor-fake + broker + dashboard`

* **RealTime Chat & Location App (React Native + Socket.IO + Maps)** — *Chat & share lokasi*.
  `power: socket + geolocation + map`

* **REALTIME‑LOKASI (Web)** — *Marker & tracking real‑time*.
  `power: leaflet + ws`

* **Sistem Manajemen Kantor (Fork)** — *Belajar UI/arsitektur*.
  `power: crud + auth`

---

## 🐍 Bonus Animasi: Snake dari Kontribusi

1. Tambah workflow berikut di repo profil (`alviansyahburhani/.github/workflows/snake.yml`):

```yaml
name: Generate Snake
on:
  schedule: [{cron: "0 0 * * *"}]  # setiap hari
  workflow_dispatch:
  push: {branches: [main]}
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: Platane/snk@v3
        with:
          github_user_name: alviansyahburhani
          outputs: |
            dist/snake.svg
      - uses: actions/upload-artifact@v4
        with: {name: snake, path: dist/snake.svg}
      - uses: actions/checkout@v4
      - name: Commit snake
        run: |
          mkdir -p assets
          cp dist/snake.svg assets/snake.svg
          git config user.name "github-actions"
          git config user.email "github-actions@github.com"
          git add assets/snake.svg
          git commit -m "chore: update snake" || echo "no changes"
          git push
```

2. Sematkan ke README:

```md
<p align="center"><img src="assets/snake.svg" alt="snake" /></p>
```

---

## 📈 Stat Keren (Auto‑update)

<p>
  <img src="https://github-readme-stats.vercel.app/api?username=alviansyahburhani&show_icons=true&hide_title=true&count_private=true" height="160" />
  <img src="https://github-readme-streak-stats.herokuapp.com?user=alviansyahburhani" height="160" />
</p>
<p>
  <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=alviansyahburhani&layout=compact" height="160" />
</p>

---

## 🕹️ Mini‑Game di GitHub Pages (opsional, beneran bisa dimainkan)

1. Buat repo: `alviansyahburhani.github.io` → branch `main`.
2. Buat file `index.html` sederhana game “Avoid the Bug” (canvas). **Salin kode ini:**

```html
<!DOCTYPE html><html lang="id"><meta charset="utf-8"/><title>Alvian — Mini Game</title>
<canvas id="c" width="420" height="320" style="background:#0b1020;display:block;margin:24px auto;border-radius:12px"></canvas>
<script>
const cvs=document.getElementById('c'),ctx=cvs.getContext('2d');
let px=40,py=150,vy=0,score=0,alive=true,bugs=[];const G=0.6,J=-9;let t=0;
function spawn(){const y=40+Math.random()*240;bugs.push({x:420,y, vx:-(2+Math.random()*3), r:10});}
function input(e){if(!alive){reset();return} if(e.code==='Space'){vy=J;e.preventDefault();}}
function reset(){px=40;py=150;vy=0;score=0;alive=true;bugs=[];t=0;}
addEventListener('keydown',input);
function loop(){t++; if(t%70===0) spawn(); vy+=G; py+=vy; py=Math.max(10,Math.min(310,py));
  ctx.clearRect(0,0,420,320);
  // player
  ctx.fillStyle='#4ade80'; ctx.beginPath(); ctx.arc(px,py,12,0,7); ctx.fill();
  // bugs
  ctx.fillStyle='#f43f5e'; bugs.forEach(b=>{b.x+=b.vx; ctx.beginPath(); ctx.arc(b.x,b.y,b.r,0,7); ctx.fill();});
  bugs=bugs.filter(b=>b.x>-20);
  // collide
  bugs.forEach(b=>{const dx=b.x-px,dy=b.y-py; if(Math.hypot(dx,dy)<(b.r+12)){alive=false}});
  // score
  if(alive){score++;}
  ctx.fillStyle='#e2e8f0'; ctx.font='16px monospace'; ctx.fillText('SCORE '+score,10,20);
  if(!alive){ctx.fillText('GAME OVER — tekan SPACE untuk retry',30,160);} 
  requestAnimationFrame(loop);
}
loop();
</script></html>
```

3. Aktifkan **Settings → Pages** (source: `main / root`).
4. Tambah tombol **Play** di profil: `[▶️ Mainkan Mini‑Game](https://alviansyahburhani.github.io)`.

---

## 📫 Kontak

[![Gmail](https://img.shields.io/badge/Gmail-D14836?logo=gmail\&logoColor=white)](mailto:alviansyahburhani@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin\&logoColor=white)](#)

---

### Cara Pasang (ringkas)

1. Buat **repo profil** bernama `alviansyahburhani` → taruh README *Game Mode* ini.
2. **Pin 6 proyek** paling keren.
3. Tambah **Snake workflow** & sematkan `assets/snake.svg`.
4. (Opsional) Buat **mini‑game Pages** lalu tambahkan tombol Play.

> Selamat datang di profil yang bisa dimainkan. Have fun! ✨

---

## 📄 Template 2 — Classic Developer Style (final untuk Alvian)

> **Salin persis** ke `README.md` repo profil `alviansyahburhani`. Struktur dan urutan sudah disamakan dengan contoh screenshot. Ganti link sosial yang masih placeholder (#) bila ada.

```md
<h1 align="center">Hi 👋, I'm Alvian Syah</h1>
<p align="center">A passionate website developer from Indonesia</p>

<p align="center">
  <img src="https://komarev.com/ghpvc/?username=alviansyahburhani&label=Profile%20views&color=0e75b6&style=flat" alt="views"/>
</p>

- 🌱 I’m currently learning **MERN stack**  
- 📝 I regularly write articles on **https://medium.com/@alviansyahburhani**  
- 📫 How to reach me **alviansyahburhani@gmail.com**

### Connect with me:
<p>
  <a href="mailto:alviansyahburhani@gmail.com"><img src="https://img.shields.io/badge/Gmail-D14836?logo=gmail&logoColor=white"/></a>
  <a href="#"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white"/></a>
  <a href="https://medium.com/@alviansyahburhani"><img src="https://img.shields.io/badge/Medium-12100E?logo=medium&logoColor=white"/></a>
  <a href="#"><img src="https://img.shields.io/badge/YouTube-FF0000?logo=youtube&logoColor=white"/></a>
  <a href="#"><img src="https://img.shields.io/badge/Instagram-E4405F?logo=instagram&logoColor=white"/></a>
</p>

---

## TECHSTACKS 🧙‍♂️

**Languages:**  
<img src="https://skillicons.dev/icons?i=c,js,ts,py,php" height="36"/>

**Front‑End:**  
<img src="https://skillicons.dev/icons?i=html,css,js,ts,react,nextjs,tailwind,bootstrap,wordpress" height="36"/>

**Back‑End & Databases:**  
<img src="https://skillicons.dev/icons?i=nodejs,express,postgres,mysql,mongodb,firebase,supabase" height="36"/>

**Tools:**  
<img src="https://skillicons.dev/icons?i=git,github,postman,vscode,androidstudio,figma,vercel,netlify" height="36"/>

---

## GitHub Stats ✨

<p>
  <img src="https://github-readme-stats.vercel.app/api?username=alviansyahburhani&show_icons=true&locale=en" height="160"/>
  <img src="https://github-readme-stats.vercel.app/api/top-langs?username=alviansyahburhani&show_icons=true&locale=en&layout=compact" height="160"/>
</p>

<p>
  <img src="https://github-readme-streak-stats.herokuapp.com/?user=alviansyahburhani" height="180"/>
</p>

<!-- Trophies (opsional) -->
<p>
  <img src="https://github-profile-trophy.vercel.app/?username=alviansyahburhani&theme=onedark&row=1&column=6"/>
</p>

<!-- Wakatime (opsional) -->
<!--
<p>
  <img src="https://github-readme-stats.vercel.app/api/wakatime?username=YOUR_WAKATIME&layout=compact" height="260"/>
</p>
-->
```

**Yang perlu kamu sesuaikan:**

* Ganti tautan **LinkedIn/YouTube/Instagram** (yang masih `#`).
* Jika tidak pakai Medium, ubah/ kosongkan barisnya.
* Jika pakai Wakatime, ganti `YOUR_WAKATIME`.
