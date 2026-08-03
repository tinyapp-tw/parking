# 停車定位（PWA）

記下車輛停放位置的個人工具。PWA 形式，免費、不需上架、資料只存手機本機。

## 功能

- **一鍵記位置**：按下大按鈕取得 GPS 座標並記住
- **導航回車上**：顯示與車子的即時直線距離，一鍵開 Apple 地圖 / Google 地圖步行導航
- **室內模式**：地下停車場收不到 GPS 時，改用拍照（柱號）+ 樓層文字備註
- **停車計時**：顯示已停多久；可選填每小時費率，自動估算費用
- **離線可用**：記錄與查看不需網路（開地圖導航需要網路）

## 檔案結構

| 檔案 | 用途 |
|---|---|
| `index.html` | 整個 App（HTML + CSS + JS） |
| `manifest.webmanifest` | PWA 設定 |
| `sw.js` | Service Worker（離線快取） |
| `icons/` | App 圖示 |
| `serve.py` | 本機開發伺服器 |

## 本機測試

```bash
python serve.py 8124
```

瀏覽器開 <http://127.0.0.1:8124>（定位功能需要 HTTPS 或 localhost 才會生效）。

## 部署

與 subman 相同：GitHub repo → Settings → Pages → Deploy from a branch（main / root）。

## 安裝到 iPhone

Safari 開啟部署網址 → 分享 → 加入主畫面。第一次按「記下停車位置」時 iPhone 會詢問定位權限，選「允許」。

## 已知限制

- **地下室 GPS**：物理限制，收不到訊號時請用室內模式（照片 + 備註）；精度差於 100 公尺時 App 會主動警告
- **Safari 與主畫面 App 資料不相通**：iOS 隔離兩者的儲存空間，安裝後請固定從主畫面圖示開啟（App 內有提示）
- **拍照時若系統回收頁面**：極少見（記憶體不足時），照片可能沒存到；App 重開時會偵測並提醒重拍
- **冷啟動短暫白屏**：iOS 不支援 manifest 的啟動畫面設定，完整解法需為各機型產生 startup image，成本高暫不處理
