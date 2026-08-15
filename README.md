# dsh-wallpaper-rotator (Enhanced)

DeepSeek Harness (dsh) Web UI 壁纸轮换插件 —— 基于 [liceses/dsh-wallpaper-rotator](https://github.com/liceses/dsh-wallpaper-rotator) 的二开增强版。

> 原版 MIT License © 2025 dsh-wallpaper-rotator contributors。本二开保留原版权声明。

## 相比原版的增强

### 🎬 视频背景支持(原版只支持图片)

- 文件夹里的 `mp4 / webm / mov / m4v` 视频也能作为背景壁纸,自动循环静音播放
- 图片与视频在轮换中无缝切换(淡入淡出)
- host 端新增 **Range 请求(206 Partial Content)+ 流式传输**,视频 seek/拖动进度条不卡顿
- 单视频上限放宽到 1GB(图片仍为 64MB)

### 🖼️ 整页壁纸(原版只覆盖对话框区域)

- 新增**表面中和(surface neutralization)**:遍历 DOM,自动把大尺寸不透明面板(侧边栏、文件树、绘画面板、输入条、渐变灰条等)的背景清为透明,让壁纸铺满整个页面
- 识别纯色 / 半透明 / 渐变背景,含细长横条规则(宽 ≥ 半屏且高 ≥ 6px)
- `data-wp-neutralized` 标记 + CSS `!important` 兜底,React 重渲染不会重置透明度
- 弹窗 / 模态(高 z-index)保持不透明,保证可读性

### 🛠️ dsh rc.6 兼容修复

- 原版依赖已废弃的 client `timer` 服务(`ctx.interval / ctx.timeout / ctx.debounce`),在 rc.6 上无法加载
- 二开全部改为原生 `setInterval / setTimeout / 自实现 debounce`,inject 收敛为 `["slots", "theme"]`

## 安装

```powershell
# 本地路径
dsh plugin --profile web add C:\path\to\dsh-wallpaper-rotator
# 或 GitHub(发布后)
dsh plugin --profile web add github:<user>/dsh-wallpaper-rotator
```

重启 `dsh web` 后,设置 → 壁纸轮换 即可配置。

## 配置

- 文件夹路径(图片 + 视频)、轮换间隔(秒/分/时)、顺序/随机
- 面板透明度、壁纸压暗、毛玻璃模糊(0-24px)、文字阴影(三档)
- 配置持久化到 `$DSH_HOME/wallpaper-rotator.json`

## License

MIT — 原版权归 dsh-wallpaper-rotator contributors 所有。
