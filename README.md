# LYS 美妍 SPA 館 官網 — 部署說明

## 檔案結構
```
lys-spa-deploy/
├── index.html              # 主頁：品牌敘事、療程、節氣、門市、進站彈窗輪播
├── promotions.html         # 當期活動：新客體驗、奢寵組合
├── membership.html         # 會員制度（已完整填入內容）
├── academy.html            # 撥經教學招生（部分內容待補）
├── styles.css              # 共用樣式表
└── assets/                 # 圖檔資源
```

## 進站彈窗輪播（index.html）

每次首頁載入後約 0.8 秒自動彈出，三張輪播：
1. 當令節氣資訊卡（穀雨）
2. 新客體驗 1,280 活動圖
3. 奢寵組合 2 小時撥經活動圖

操作：6 秒自動切換、可手動點左右箭頭或下方圓點、點 × 或背景或按 ESC 關閉。
點活動圖會連到 promotions.html 對應活動錨點。點節氣卡連到 #seasonal。

若日後不想每次都彈出，可在 index.html 的彈窗 JS 最後加入：
```javascript
if (sessionStorage.getItem('modalSeen')) return;
sessionStorage.setItem('modalSeen', '1');
```
放在 `setTimeout(openModal, 800)` 之前。

## 節氣內容更新

每個節氣轉換時需要更新的位置：
- `index.html` 頂部 `.season-tag` 的文字
- `index.html` 中 `.seasonal` 整個區塊
- `index.html` 進站彈窗 `slide-season` 中的節氣名、日期、詩句、四格小卡

## 活動更新

活動變動時需要更新：
- `promotions.html` 文案與 CTA
- `index.html` 的 `.promo-strip` 區塊（兩張活動卡）
- `index.html` 進站彈窗的兩張活動 slide
- `assets/` 資料夾中的 promo-*.jpg 圖檔

## 待補充內容

### academy.html — 撥經教學招生
- 課程堂數 / 週數 / 結業認證（目前顯示 {X}）
- 四大模組實際課程內容
- 下期開課日、上課地點、學費、早鳥或分期方案、招生人數

placeholder 以 `{中括號}` 標示。

## 部署方式

上傳整個 `lys-spa-deploy/` 資料夾到任何靜態主機即可。
所有頁面之間使用相對路徑連結，無需額外路由設定。

## 瀏覽器相容性

支援 Chrome、Safari、Firefox、Edge 及行動裝置。
