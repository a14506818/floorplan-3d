# 三房一廳雙衛 · 室內設計方案

套內約 41 m²（12.4 坪）的 2D 配置 + 3D 漫遊，以設計公司的平面與立面圖為底（原始圖檔不公開）。

- 線上版：https://a14506818.github.io/floorplan-3d/
- 設計細節、指定設備、待確認清單、修改紀錄：[DESIGN.md](DESIGN.md)

## 快速開啟

```bash
python3 -m http.server 8000
```

開 http://localhost:8000，按 `T` 切 3D。

| 按鍵 | 作用 |
| --- | --- |
| `T` | 切換 2D / 3D |
| `V` / `M` / `X` | 選取 / 測量 / 拆改牆體 |
| `R` / `Shift+R` | 家具旋轉 90° |
| `Ctrl/⌘ + Z` | 復原 |
| 漫遊：`WASD`、`E` | 移動、開關門 |

## 修改資料

全部在 `index.html`：

- 格局：`WALLS`、`WINS`、`DOORS`、`SLIDES`、`ROOMS`
- 預設家具：`defaultFurniture()`；`elev` ＝離地高度（mm）
- 自訂家具：2D 在 `furnSVG()`、3D 在 `buildFurniture()`
- 材質：`CAB_STYLE`（由全屋配色 `THEME` / `state.theme` 在 3D 建模前寫入；2D 木色用 `TW()`）、`plasterMat()`、`mirrorMesh()`；個別家具顏色色票在 `SWATCHES`；門片把手 `fronts(…, 'bar' | 'edge' | 'alu' | 'aluB')`
- 隱藏門：`DOORS` 的 `slat`（木格柵）/ `paint`（塗料）
- **樣式 / 狀態**：在 `VARIANTS` 宣告某種家具有哪些選項（`label`、`values`、`def`；`click:true` ＝ 3D 點一下輪替；`when` ＝ 只在條件成立時適用），選的值存在 `f.opts`；繪圖時用 `optOf(f, key)`（3D）/ `ov(key)`（2D `furnSVG`）讀取。屬性面板會自動出現「樣式」按鈕。同一件家具的不同版本用「款式」選項，不要另開新類型；舊類型在 `TYPE_MERGE` 轉換

**存檔**：擺設存在各自瀏覽器的 localStorage，不會同步。改了 `defaultFurniture()` 後舊存檔自動作廢，可從「文件 → 還原舊存檔」找回。要把頁面上的擺法設成預設：文件 → 匯出方案 JSON，再轉寫進 `defaultFurniture()`。

**更新線上版**：`git add -A && git commit -m "…" && git push`，1–2 分鐘後 GitHub Pages 自動更新。

---

工具來自 [wy51ai/floorplan-3d](https://github.com/wy51ai/floorplan-3d)（MIT），原始說明見 [README.en.md](README.en.md)。
