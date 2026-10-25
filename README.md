# 光学行业新闻热点

手机镜头、MR、增距镜、无人机、运动相机及舜宇光学同行动态的移动端新闻页，优先官方来源。

公网地址：https://ningtaolu.github.io/optics-news/

## 结构

| 文件 | 作用 |
|---|---|
| `index.html` | 页面（内联 CSS/JS，无任何依赖），首页 = 今日头条 + 分类入口，`#/分类名` 进入列表 |
| `news.json` | 新闻数据：`updated`、`categories`、`headlines`（今日头条说明）、`note`（本期说明）、`brief`（一分钟简报，3-5 条）、`items`（每条含 `impact:{dir:利好/利空/中性,text}` 与 `takeaway`，均为**分析判断**，非新闻事实；`title` 结论先行） |
| `ticker.json` | 可选：首页「数据速览」，`items[{id,label,value,delta,dir,asof,source}]`；只能引用 `news.json` 已有条目中的数字（`id` 必须存在），标注日期与「非实时」 |
| `risks.json` | 风险观察：`updated`、`subs`（政策与地缘 / 上下游供应链 / 宏观经济 / 竞争格局）、`items` |
| `icon.png` | 网站图标 / 添加到主屏幕图标 |
| `.nojekyll` | 让 GitHub Pages 原样发布 |

## 更新

只改 JSON 即可：在 `items` 中追加条目，并更新 `updated`。页面每次打开都会以 `no-store` 方式重新拉取 JSON。

新闻条目字段：`id, date(YYYY-MM-DD), cats[], title, summary, source, url, official(bool), tags[], headline?(1-3), background?(bool)`。

风险条目字段：`id, date, sub, title, summary, impact(利空/利好/中性), severity(高/中/低), source, url`。

## 本地预览

```sh
python3 -m http.server 8000   # 打开 http://localhost:8000/
```

## 发布到 GitHub Pages

推送到 `ningtaolu/optics-news` 的 `main` 分支，Settings → Pages → Source 选 “Deploy from a branch”，分支 `main`、目录 `/ (root)`。


## v2 功能（2026-10-25）
顶部可横滑频道栏、底部 Tab（要闻/快讯/风险/收藏）、一分钟简报、头条大卡、数据速览、按日期分组的快讯时间轴（头条标红）、已读/「新」标记与未读数、收藏（稍后读）、站内搜索（关键词高亮）、标签专题页 `#/标签/名称`。已读、收藏、新条目记录仅存于本机 localStorage。路由：`#/要闻`、`#/快讯/分类`、`#/风险`、`#/收藏`、`#/搜索/词`、`#/标签/名`（兼容旧的 `#/分类名`）。
