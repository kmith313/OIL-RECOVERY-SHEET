# OIL-RECOVERY-SHEET
Standalone Oil Recovery Sheet app — separated out from the Wire & Strip Stock Dashboard.

## Kya hai isme
- Sirf **Oil Recovery Sheet** feature: Transformer Repaired / DTC entry, Oil Balance
  (Fresh / B&C / Reclaim), strict auto carry-forward, XEN-only Recovery Standards,
  Date Range Summary, aur Excel export.
- Item Master, Receive/Issue log, aur Wire-Strip Stock Dashboard is app me **nahi** hai —
  wo purani app (Wire & Strip Stock Dashboard) me hi rahenge.

## Data save kaise hota hai
- Same Google Sign-In (same CLIENT_ID) + Google Drive auto-sync (har 3 second me), bilkul
  pehle jaisa mechanism.
- **Naya, alag Drive folder** use hota hai (Folder ID: `1eLF24RHGr83tp_FdxkLjWdHewX6Smqct`)
  — is app ka data purani Wire & Strip Dashboard ke folder se bilkul alag rehta hai, taaki
  dono apps ek dusre ki files overwrite na karein.
- ZAROORI: Ye naya folder Google Drive me sabhi workers (jo is app se sign-in karenge) ke
  saath Editor access se share hona chahiye, warna unki entries save nahi ho payengi.
  (Folder kholo -> Share -> jo bhi emails use karni hain unhe "Editor" access do.)
- Har worker ki entry `oil_recovery_data_<email>.json` naam ki file me is naye folder me
  save hoti hai.
- Recovery Standards `oil_recovery_standards.json` file me isi naye folder me save hoti hain.
- XEN (admin) "All Workers Combined" view me sabhi workers ki `oil_recovery_data_*.json`
  files ko is naye folder se real-time me jodta hai.

## ZAROORI SETUP STEPS

### 1. Naye Drive folder ko share karo
Folder ID `1eLF24RHGr83tp_FdxkLjWdHewX6Smqct` ko Google Drive me kholo, "Share" dabao,
aur jitne bhi workers/XEN is app ko use karenge unke Google account emails ko
**Editor** access do. Bina iske koi bhi worker apni entry save nahi kar payega.

### 2. App ko ALAG folder/URL par host karo
Is app ko purani Wire & Strip Dashboard wale **exact same URL/folder me mat daalo** —
dono apps ke file names (index.html, sw.js, manifest.json) same hain, isliye same
folder me daalne se ek dusre ko overwrite kar dete hain aur Service Worker cache
conflict ki wajah se Sign-In tak kaam karna band ho jaata hai.
Isse alag subfolder ya alag hosting URL par rakho, jaise:
- `yoursite.com/wire-strip/` -> purani Stock Dashboard
- `yoursite.com/oil-recovery/` -> ye nayi Oil Recovery Sheet

### 3. CLIENT_ID authorized origin
Jis bhi domain par host karo (jaise `yoursite.com`), wo domain Google Cloud Console me
is CLIENT_ID ke "Authorized JavaScript origins" me already add hona chahiye:
1. https://console.cloud.google.com/apis/credentials
2. OAuth 2.0 Client ID `933740281356-2gf56thakcjdprj45n93nsc3dl2353bk...` kholo
3. "Authorized JavaScript origins" me apna domain check/add karo aur Save karo

## Files
- `index.html` — poora app (UI + logic)
- `manifest.json` — PWA manifest ("Install App" ke liye)
- `sw.js` — offline caching service worker
- `icon-192.png`, `icon-512.png` — app icons
