# MBTI 16 型人格测试（48 题版）

纯静态网页，零依赖，手机 / 电脑 / 平板都能直接打开。

线上地址：`https://<你的用户名>.github.io/mbti-test/`

## 目录结构

```
index.html        页面结构（首页 / 答题 / 结果 / 数据分析 四个视图）
css/style.css     样式（暗色 + 霓虹渐变）
js/data.js        题库 48 题 + 四个维度 + 16 型人格文案
js/app.js         随机抽题、四维度计分、结果渲染、本地统计
.nojekyll         跳过 GitHub Pages 的 Jekyll 构建，保证文件原样发布
```

## 本地预览

```powershell
powershell -ExecutionPolicy Bypass -File .\tools\serve.ps1
```

然后打开 <http://localhost:8000>。

## 计分规则

- 四个维度：**E/I**（能量来源）、**S/N**（获取信息）、**T/F**（决策方式）、**J/P**（生活态度）
- 每个维度 12 题，共 48 题
- 每题两个选项，分别对应维度的一极；统计每极得票数 → 算百分比 → 多数决得出四字母类型
- 题目顺序与 A/B 选项位置**每次随机**，避免位置暗示
- 第 31 题为反向量表（先"情感"后"逻辑"），在数据里用 `first: 'F'` 单独标注，不会算反

## 改内容

| 想改什么 | 改哪里 |
| --- | --- |
| 题目 / 选项 | `js/data.js` 的 `QUESTIONS`，`first` 字段表示选项 A 属于哪一极 |
| 16 型文案 | `js/data.js` 的 `TYPES`（desc / good / bad / careers / tags） |
| 配色 | `css/style.css` 顶部 `:root` 的变量 |
| 题量 | 增删 `QUESTIONS` 数组条目，计分自动按实际题数算 |

## 数据说明

- 每次测试结果存在浏览器 `localStorage`（键名 `mbti_records_v1`），**不会上传服务器**
- 「数据分析」页可看类型分布排行、四维度平均倾向，支持导出 CSV、载入示例数据、一键清空

## 更新到线上

```powershell
git add -A
git commit -m "更新内容"
git -c http.sslBackend=schannel push origin main
```

推送后 1~2 分钟 GitHub Pages 自动刷新。

> 说明：题库取自公开流传的 MBTI 48 题基础版（jingyunce.com），仅作课程演示与自我探索参考，非心理诊断工具。
