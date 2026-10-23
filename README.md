# 凯凯 × 拖鞋 的专属扫雷乐园

一个单文件、纯前端的扫雷小游戏，可以直接部署到 GitHub Pages，也可以嵌进个人网站的 iframe。

- 默认棋盘：**20 × 20，80 颗雷**
- 单机模式：随机雷盘，第一格安全
- 对战模式：共享种子生成完全相同的雷盘，各自计时
- 无框架、无 CDN、无外部字体、无广告、无后端
- 不使用 localStorage / sessionStorage，不保存游戏数据

## 直接运行

双击 `index.html`，用浏览器打开即可。

## 部署到 GitHub Pages

1. 新建一个 GitHub 仓库。
2. 把 `index.html` 放到仓库根目录。
3. 打开仓库的 **Settings → Pages**。
4. Source 选择 **Deploy from a branch**，Branch 选择 `main` 和 `/ (root)`，保存。
5. 等 GitHub Pages 构建完成后，访问生成的网址。

## 嵌入个人网站

把 `src` 换成你部署后的地址即可：

```html
<iframe
  src="https://你的用户名.github.io/你的仓库名/"
  title="凯凯 × 拖鞋 的专属扫雷乐园"
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

- **默认单机棋盘 / 雷数**：修改 `index.html` 中的 `DEFAULT_GAME`，以及自定义表单的初始 `value`。
- **对战棋盘 / 雷数**：修改 `BATTLE_GAME`。为了种子公平，对战模式固定使用 20×20 / 80 雷。
- **换成别的图标**：修改文件顶部的 SVG `<symbol>`，例如 `icon-panda`、`icon-slipper`。
- **改文案**：搜索「太棒啦」「ohno」「可以再来一局哦」等中文文案即可。
- **颜色**：修改 CSS 顶部 `:root` 里的颜色变量。

## 操作

- 左键：翻开格子
- 右键：放置 / 收起小拖鞋标记
- 手机：轻点翻开，长按放 / 收小拖鞋
- 键盘：方向键移动，`F` 放 / 收小拖鞋，`Enter` / `空格` 翻开
