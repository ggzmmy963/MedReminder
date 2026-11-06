# 浏览器本地 OCR 资源

这是网页版「识别说明书并自动填写」使用的本地 OCR 资源目录。不要把本目录拆开或改名。

## GitHub Pages 部署

把整个 `ocr/` 文件夹上传到 GitHub Pages 仓库根目录，和 `index.html` 放在同一级：

```text
你的仓库/
├── index.html
├── .nojekyll
└── ocr/
    ├── tesseract.min.js
    ├── worker.min.js
    ├── tesseract-core-lstm.wasm.js
    ├── tesseract-core-simd-lstm.wasm.js
    ├── lang/
    │   └── chi_sim.traineddata.gz
    └── LICENSE-*.txt
```

访问：

```text
https://你的用户名.github.io/你的仓库/
```

页面会使用相对路径 `ocr/...` 加载资源，不需要本地代理，也不需要服务器。

## 文件说明

- `tesseract.min.js`：Tesseract.js 5.1.1 浏览器入口
- `worker.min.js`：OCR worker
- `tesseract-core-lstm.wasm.js`：非 SIMD 核心，兼容性优先
- `tesseract-core-simd-lstm.wasm.js`：SIMD 核心，支持的设备会自动使用
- `lang/chi_sim.traineddata.gz`：中文简体语言包，约 19MB

首次点击识别时需要加载约 25MB 资源，页面会显示进度。加载完成后浏览器会缓存，后续会快很多。

## 注意

- 照片只在本机浏览器内处理，不会上传到服务器。
- 手机端识别速度和准确率取决于设备性能与照片清晰度。
- 如果 `ocr/` 目录缺失，页面会提示检查资源是否上传完整。
- 本项目不再依赖 `proxy-server.mjs` 做网页 OCR；该代理仅保留给本地 AI 或插件版 OCR。
- Tesseract.js 与 Tesseract core 使用 Apache 2.0 许可；语言包来自 Tesseract tessdata，使用 Apache 2.0 许可。
