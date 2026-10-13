# 📋 PROJECT CONTEXT — Dashboard Monitoring PLTS Biznet Power
*Status: BASE v2.2 — full-stack production (GitHub Pages + Apps Script + Google Sheets)*

## 🎯 Arsitektur
- **Frontend**: trial.html — GitHub Pages
  https://facilitybiznetpower-commits.github.io/My-Dev/
- **Backend**: Google Apps Script Web App — project "Biznet Power API" (file BizNetPowerAPI.gs)
  URL /exec tersimpan di CONFIG.API_URL dalam trial.html
- **Database**: Google Spreadsheet ID: 1doEoT0SIW5KBKD5Qwi3LYXvZPn0AgXuaU_toFhoyoM0
  Tab: "Prep : Data Survey Site", "Prep : PR/PO ", "Prep : Delivery Material",
  "Prep : Tools", "Prog : Team Biznet Power", "REPORT DONE", "STOCK MATERIAL",
  "Photos" (auto-create oleh script)
- **Foto**: Drive folder "FOTO REPORT" (ID: 1pd3alQl4z9cSJqUtaVhP2fv3CyM6R0cD)
- **Manifest**: appsscript.json dengan oauthScopes: spreadsheets + drive

## 🖥️ Fitur trial.html (BASE v2.2)
- 5 tab: Overview (peta Leaflet Esri + Chart.js), Instalasi (On Progress/Done Live),
  Site Survey, PR/PO, Material & Tools (Delivery/Stok/Tools)
- 5 kartu Overview COMPACT (padding 6px, angka 18px) agar peta langsung terlihat
- Kartu "Kapasitas Terpasang": kWp DIBULATKAN 1 desimal (Math.round(x*10)/10),
  sub-text hanya "n panel terpasang" (tanpa kVA/kWh)
- Edit Progres ✏️ → saveProgress → tab Prog (8 tahap D/P/R/. → % otomatis:
  Done=12,5% • Progress=6,25%; 100%=Done, 1-99%=On Progress, 0%=Prepare)
- Edit Delivery ✏️ → saveDelivery → tab Delivery (DONE/PARTIAL(n/5)/BELUM)
- Tombol simpan bernama "💾 Save"; toast singkat ("Progres tersimpan ✅")
- Header bersih: judul + tombol 🔄 Refresh Data saja (footer sudah dihapus)
- Foto 📷 → uploadPhoto (JPEG maks 1600px) → Drive + register tab Photos;
  hapus foto = trash file + hapus baris register
- Lightbox fullscreen: klik foto terisi → zoom 100vw/100vh, klik/✕ tutup
- Modal dokumentasi 880px, slot foto 200px
- Info PV (pill ☀️): On Progress = "Plan PV: n panel ≈ x kWp" (dari Survey ×0,64),
  Done Live = "PV Terpasang: pcs • kWp | Inverter kVA • Battery kWh"
- PDF report jsPDF (A4, navy header, data + 4 foto dari Drive via getPhoto base64)
- RO2REG: RO09/10/11/22=JATIM, BALI 1/2/3=BALI, RO07/08/20/21=JATENG

## ⚙️ Endpoints Apps Script
- GET  ?action=ping (ada ver:"v2-patch") | getAll | getPhoto&id=FILEID
- POST {action: saveProgress|saveDelivery|uploadPhoto|deletePhoto, ...}
- Deploy: Execute as Me • Access Anyone
- Fungsi diagnostik: setupCheck, testDrive (TANPA try/catch!), testUpload, createPhotosTab

## 📝 Pelajaran Troubleshooting (jangan diulang!)
1. Edit Code.gs → WAJIB Deploy → Kelola deployment → ✏️ → Versi baru
2. openById butuh ID murni bukan URL (patch regex ada di ss() & getPhotoFolder())
3. Jangan ada fungsi/konstanta duplikat di file .gs
4. try/catch pada fungsi tes MENELAN popup otorisasi → biarkan error terlempar
5. Sukses di editor ≠ Web App sudah pakai kode/izin baru → WAJIB deploy versi baru
6. Scope Drive ditambahkan via appsscript.json oauthScopes
7. Penjumlahan float JS bisa menghasilkan desimal panjang → selalu Math.round

## ⚠️ TODO / Keterbatasan
- [ ] KEAMANAN: API_URL terekspos di repo publik — siapa pun bisa baca/tulis
      spreadsheet. RENCANA: token rahasia di doGet/doPost + CONFIG.TOKEN di HTML
- [ ] Tab Survey/PRPO/Report/Stock/Tools masih read-only di dashboard
- [ ] Belum ada: export Excel, timeline tanggal per tahap, log aktivitas

## 🔄 Cara Pakai File Ini
Di chat baru: paste isi file ini + attach trial.html (dan Code.gs bila perlu)
→ AI langsung paham konteks, tidak perlu setup ulang.
