# 图片转 PCB 艺术板

`image-to-pcb-art` 是一个 Codex Skill，指导将插画或线稿制作成嘉立创EDA中的 PCB 艺术板。它涵盖彩色丝印、铜层与阻焊开窗的分层、图像导入、轮廓清理、叠层核对和制板文件检查。

## 适用范围

适合把角色插画、装饰图案或线稿放到 PCB 上，以及修改已有艺术板的图层和边缘。普通电子电路设计与审查不在本 Skill 的范围内。

## 关键规则

- 顶层彩色丝印默认使用完整原图。即使同一区域另有顶层铜和阻焊开窗，也不自动从丝印图片中扣除这些区域。
- 需要金属效果时，从原图单独提取轮廓，在同面铜层和阻焊层制作对齐的图形。
- 对需要露铜的金线，沿原图重绘 SVG 闭合路径，用贝塞尔曲线修顺断口和转角，再从同一份 SVG 生成顶层铜与顶层阻焊开窗。
- 只有明确要求丝印让出金属区域时，才为彩图制作透明区。
- 成品尺寸、正反面内容和金属区域以每次任务的要求为准，不沿用示例工程的尺寸。

完整流程见 [SKILL.md](SKILL.md)。

## 安装

将此仓库克隆到 Codex 的个人 Skill 目录：

```powershell
git clone https://github.com/violetlily/image-to-pcb-art.git "$HOME\.codex\skills\image-to-pcb-art"
```

安装后的目录结构为：

```text
~/.codex/skills/image-to-pcb-art/
├── SKILL.md
└── README.md
```

在 Windows 上，可将 `~/.codex/skills` 理解为 `%USERPROFILE%\.codex\skills`。安装后可在对话中使用 `$image-to-pcb-art` 调用。

在嘉立创EDA前台自动操作时，Skill 会优先参考另行安装的 `easyeda-api` Skill；没有连接时也可以按界面流程完成。

## 调用示例

> 使用 `$image-to-pcb-art`，把这张插画绘制到已打开的 PCB。成品为 60 × 100 mm，正面保留完整彩色原图；把指定的金色装饰制作成顶层铜和阻焊开窗，最后核对并导出彩色丝印制板文件。

导出供制造使用的文件前，还应按目标板厂的当前工艺要求核对最小线宽、间距、板材、阻焊颜色和生产预览。
