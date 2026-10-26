# 凯神的扫雷乐园

**线上地址：** https://yscc666.github.io/kaikai-tuoxie-minesweeper/

一个单文件、纯前端的扫雷小游戏，已经部署到 GitHub Pages，也可以嵌进个人网站的 iframe。

- 默认棋盘：**20 × 20，40 颗雷**
- 单机模式：首点安全，只采用「靠逻辑推理就能推完、不需要猜」的雷盘
- 对战模式：共享种子生成完全相同的雷盘，双方从同一个亮框起点开始，各自计时
- 视觉：近黑底 + 深蓝强调色 + 玻璃卡片；页头是一张小熊猫抱苹果的照片，背景是它的虚化光晕
- 小熊猫 = 地雷，苹果 = 标记
- 无框架、无 CDN、无外部字体、无广告、无后端；样式、脚本、图片全部内嵌在 `index.html` 里
- 不使用 localStorage / sessionStorage，不保存游戏数据

## 直接运行

双击 `index.html`，用浏览器打开即可。

## GitHub Pages

当前版本已经发布在 GitHub Pages。若之后更新了 `index.html`：

1. 把新的 `index.html` 放到仓库根目录（覆盖旧文件）。
2. 仓库的 **Settings → Pages** 保持 **Deploy from a branch**，Branch 为 `main`，目录为 `/ (root)`。
3. 等待 Pages 重新构建，刷新线上网址即可。

## 嵌入个人网站

把 `src` 换成你部署后的地址即可：

```html
<iframe
  src="https://你的用户名.github.io/你的仓库名/"
  title="凯神的扫雷乐园"
  style="width: 100%; max-width: 920px; height: 1200px; border: 0; border-radius: 28px;"
  loading="lazy"
></iframe>
```

## 关于跨设备对战

纯前端页面无法跨设备直接读取对方的计时，因此这里提供了两种结算方式：

1. **同一浏览器双标签页**：通过 `BroadcastChannel` 自动交换完成时间，双方都完成后自动结算。
2. **不同设备**：先完成的一方复制弹窗里的「战绩码」发给对方；对方把战绩码粘贴到弹窗中，就能自动比较双方用时并判断赢家。

两份成绩齐了以后，输赢由页面自动计算，不需要自己比大小。若要求不同设备之间完全实时、无需任何粘贴，就需要后端或 WebRTC 信令服务。

## 想改点东西

- **默认单机棋盘 / 雷数**：修改 `index.html` 中的 `DEFAULT_GAME`，以及自定义表单的初始 `value`。雷数越高，「无需猜」的盘越难生成，20×20 建议不要超过 40。
- **对战棋盘 / 雷数**：修改 `BATTLE_GAME`。为了种子公平，对战模式双方固定同一盘。
- **图标**：文件里内联的 SVG `<symbol>`——`icon-panda`（小熊猫/地雷）、`icon-slipper`（现在装的是一张苹果图片，用作标记）、`icon-clock`、`icon-refresh`、`icon-heart`。
- **页头照片 / 背景光晕**：照片在 `.hero-photo` 里的 `<img src="data:image/jpeg;base64,…">`，背景光晕在 `.page::before` 里用的是同一张图的 96px 缩略图，换图要两处一起替换。
- **颜色**：CSS 开头的 `:root` 变量（`--ink`、`--blue-soft`、`--night-*` 等），以及各组件里的深蓝 `rgba(…)` 值。
- **改文案**：搜索「太棒啦」「ohno」「小苹果」「可以再来一局哦」等中文即可。

## 操作

- 左键 / 轻点：翻开格子
- 右键 / 长按：放置 / 收起小苹果标记
- 双击已翻开的数字：周围标记数对上时快速展开
- 键盘：方向键移动，`F` 放 / 收标记，`Enter` / `空格` 翻开；`Esc` 关闭结算弹窗
