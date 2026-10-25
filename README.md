# Photo2PDF

把 iPhone 拍的文件照片轉成 PDF 的網頁工具。自動偵測文件四角，也能用手指拖曳四個角手動框選，再做透視校正把斜拍的紙拉正。

**所有處理都在你的手機或電腦瀏覽器裡完成，照片不會上傳到任何伺服器。**

*A browser-based tool that turns iPhone photos into a PDF. Auto-detects document corners or lets you drag them manually, applies perspective correction, and runs entirely on-device.*

## 功能

- 一次加入多張照片，每張變成 PDF 的一頁
- **自動框圖**：用 OpenCV.js 偵測文件邊緣，找出四個角
- **手動框圖**：點縮圖或 ✎ 進入編輯，拖曳四個角；按住時會出現放大鏡，方便對準
- **透視校正**：斜拍的文件會被拉成正的長方形
- 濾鏡：原色 / 灰階 / 增強（去陰影）/ 黑白（掃描效果）
- 調整頁面順序、旋轉、刪除
- 頁面大小：符合照片 / A4 / Letter；畫質：標準 / 高
- iPhone 上可直接「分享」到檔案、LINE、Mail 等
- 支援 HEIC（瀏覽器不支援時自動轉檔）

## 線上使用

👉 **https://nilson0606.github.io/photo2pdf/**

## 使用方式

1. 用 iPhone Safari 打開上面的網址
2. 按「＋ 加入照片」，從相簿選照片
3. 檢查縮圖，框得不準的點進去拖曳四個角
4. 按「產生 PDF」→「下載」或「分享」

想像 App 一樣使用：Safari 下方「分享」按鈕 →「加入主畫面」。

## 技術說明

| 部分 | 做法 |
|---|---|
| 介面 | 單一 `index.html`，純 HTML / CSS / JavaScript，不需要建置 |
| 文件偵測 | OpenCV.js：用多種遮罩（Canny 邊緣、亮度門檻、開/閉運算）產生候選四邊形，再以「面積 × 實心度² × 框邊內外亮度差的一致性」評分挑選 |
| 透視校正 | `getPerspectiveTransform` + `warpPerspective` |
| 去陰影 | 影像除以模糊後的背景，背景變白、文字保留 |
| PDF | 自己寫的精簡 PDF 產生器，直接嵌入 JPEG，不依賴其他函式庫 |
| HEIC | 瀏覽器無法解碼時才載入 heic2any 轉成 JPEG |

外部資源（第一次使用時從 CDN 下載，之後瀏覽器會快取）：

- [OpenCV.js 4.10](https://opencv.org/)（Apache-2.0），約 10 MB
- [heic2any](https://github.com/alexcorvi/heic2any)（MIT），只有遇到 HEIC 且瀏覽器不支援時才載入

## 本機執行

不需要安裝任何東西，直接用瀏覽器打開 `index.html` 即可。若要用手機測試區網版本：

```bash
python -m http.server 8000
```

## 已知限制

- 第一次開啟需要網路下載 OpenCV.js（約 10 MB）
- 重新整理頁面後，目前的頁面清單會清空
- 非常大量的照片（數十張高畫質）在舊款 iPhone 上可能因記憶體不足而變慢

## 授權

[MIT License](LICENSE)
