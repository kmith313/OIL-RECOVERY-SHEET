# OIL-RECOVERY-SHEET
Standalone Oil Recovery Sheet app — separated out from the Wire & Strip Stock Dashboard.

## Kya hai isme
- Sirf **Oil Recovery Sheet** feature: Transformer Repaired / DTC entry, Oil Balance
  (Fresh / B&C / Reclaim), strict auto carry-forward, XEN-only Recovery Standards,
  Date Range Summary, aur Excel export.
- Item Master, Receive/Issue log, aur Wire-Strip Stock Dashboard is app me **nahi** hai —
  wo purani app (Wire & Strip Stock Dashboard) me hi rahenge.

## Data save kaise hota hai (bilkul pehle jaisa)
- Same Google Sign-In + Google Drive auto-sync (har 3 second me).
- Same shared Drive folder (`SHARED_FOLDER_ID`) aur same Admin/XEN email use hote hain.
- Har worker ki entry `oil_recovery_data_<email>.json` naam ki file me save hoti hai
  (pehle wali app me `wire_strip_data_<email>.json` tha — sirf naam alag hai taaki dono
  apps ka data ek dusre se mix na ho).
- Recovery Standards `oil_recovery_standards.json` file me save hoti hain — same file
  jo pehle wali app bhi use karti thi, isliye standards dono jagah sync rahenge.
- XEN (admin) "All Workers Combined" view me sabhi workers ki `oil_recovery_data_*.json`
  files ko real-time me jodta hai — bilkul us pattern par jaise purani app "All Workers
  Combined" tab banata thi.

## ZAROORI SETUP STEP
Is app ko jis bhi URL/domain par host karoge (GitHub Pages, Netlify, apna server, etc.),
us URL ko Google Cloud Console me is CLIENT_ID ke **Authorized JavaScript origins** me
add karna hoga, warna "Sign in with Google" kaam nahi karega:
1. https://console.cloud.google.com/apis/credentials par jao
2. OAuth 2.0 Client ID `933740281356-2gf56thakcjdprj45n93nsc3dl2353bk...` kholo
3. "Authorized JavaScript origins" me apna naya app ka URL (jaise
   `https://yourname.github.io`) add karo aur Save karo

Agar purani Wire & Strip app aur ye nayi Oil Recovery app dono same domain/path par
already host hain, to ye step already ho chuka hoga aur kuch karne ki zaroorat nahi.

## Files
- `index.html` — poora app (UI + logic)
- `manifest.json` — PWA manifest ("Install App" ke liye)
- `sw.js` — offline caching service worker
- `icon-192.png`, `icon-512.png` — app icons
