# JAYFORYOU Web (statis, deploy ke Vercel atau Netlify)

Isi: `index.html` (seluruh aplikasi), `config.js`, `vercel.json`, `_redirects`, `_headers`.

## Vercel
1. Buka `vercel.json`, ganti semua `GANTI_IP:GANTI_PORT` dengan IP:port panel bot kamu, contoh `123.45.67.89:25565`.
2. Upload folder ini ke GitHub lalu Import di vercel.com/new (Framework: Other), atau jalankan `npx vercel --prod` di folder ini.
3. Buka domain Vercel kamu dan login dengan akun admin dari Console bot.

## Netlify
Hapus `vercel.json`, edit `_redirects` (ganti IP:port), lalu drag-drop folder ke app.netlify.com/drop.

## Kenapa lewat rewrite?
Vercel dan Netlify memakai HTTPS, sedangkan panel kamu hanya IP:port (HTTP), jadi browser memblokir pemanggilan langsung. Rewrite membuat Vercel/Netlify meneruskan /api, /media, dan /s ke panel dari sisi server. Aman, tanpa CORS, dan IP:port tidak terlihat di browser.

## Catatan
- Jangan taruh API key atau token di `config.js`, file itu publik.
- Upload besar (video banner, file manager 300 MB, ZIP deploy) lewat proxy Vercel/Netlify bisa kena batas ukuran request mereka. Ini belum bisa saya uji. Kalau gagal, beri API domain HTTPS sendiri, isi `api` di `config.js`, tambahkan domain itu ke `connect-src` pada CSP, dan set `ALLOWED_ORIGIN` di bot.
- Chat memakai polling 3 detik (bukan WebSocket) supaya cocok dengan rewrite.
