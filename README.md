# Phiyuri - Phira Chart Auto Downloader

<div align="center">

[![GitHub Actions](https://img.shields.io/github/actions/workflow/status/wiorigami/phiyuri/fetch_phira.yml?style=flat-square)](https://github.com/wiorigami/phiyuri/actions)
[![Last Commit](https://img.shields.io/github/last-commit/wiorigami/phiyuri?style=flat-square)](https://github.com/wiorigami/phiyuri)
![Repo Size](https://img.shields.io/github/repo-size/wiorigami/phiyuri?style=flat-square)

一个自动获取 Phira 音乐谱面数据并备份到 GitHub 仓库的工具

</div>

## 📋 项目简介

Phiyuri 是一个自动化工具，通过 GitHub Actions 定时从 Phira API 获取最新的音乐谱面数据（Chart），并自动保存到仓库中。这样可以实现对 Phira 谱面数据的持续备份和版本管理。

## ✨ 功能特性

- ✅ **自动定时获取** - 每日自动运行，获取最新谱面数据
- ✅ **完整数据备份** - 从 Phira API 下载完整的谱面 JSON 信息
- ✅ **智能增量更新** - 只提交有变化的文件，保持仓库整洁
- ✅ **手动触发支持** - 随时可通过 GitHub Actions 手动运行
- ✅ **无需维护** - 完全自动化，无需手动干预
- ✅ **版本控制** - 利用 Git 实现谱面数据的版本管理和历史追踪

## 🏗️ 项目结构

```
phiyuri/
├── chart/
│   └── info/
│       ├── 001.json
│       ├── 002.json
│       └── ...
├── .github/
│   └── workflows/
│       └── fetch_phira.yml
└── README.md
```

| 目录 | 说明 |
|------|------|
| `chart/info/` | 存储所有谱面数据的 JSON 文件 |
| `.github/workflows/` | GitHub Actions 工作流配置 |

## 🔄 工作流程

```
定时触发 (每日或手动)
    ↓
连接 Phira API
    ↓
获取最新谱面列表 (按更新时间排序)
    ↓
提取所有谱面 ID
    ↓
下载每个谱面的完整 JSON 数据
    ↓
保存到 chart/info/{chart_id}.json
    ↓
检查文件变化
    ↓
自动提交并推送更新
```

## 🚀 使用方法

### 自动运行

工作流默认配置为每天自动运行。你可以在项目的 Actions 页面查看运行状态和历史记录。

### 手动触发

1. 进入 [GitHub Actions](https://github.com/wiorigami/phiyuri/actions)
2. 选择对应的工作流
3. 点击 **Run workflow** 按钮
4. 工作流将立即开始执行

### 查看数据

- 所有谱面数据保存在 `chart/info/` 目录中
- 每个文件对应一个谱面，文件名为谱面 ID
- 文件内容为 JSON 格式，包含谱面的完整信息

## 📊 API 数据源

该项目基于以下 Phira 公开 API：

| 端点 | 说明 |
|------|------|
| `https://api.phira.cn/chart` | 获取谱面列表 |
| `https://api.phira.cn/chart/{id}` | 获取指定 ID 的谱面详细数据 |

查询参数：
- `page=1` - 分页号（默认获取第一页）
- `order=-updated` - 按更新时间倒序排列

## ⚙️ 配置说明

工作流配置文件：`.github/workflows/fetch_phira.yml`

### 触发条件

- **Schedule**: 每天自动运行（可通过 `cron` 表达式自定义）
- **Manual Trigger**: 支持手动触发 `workflow_dispatch`

### 环境要求

- ✓ GitHub Actions 已启用
- ✓ 仓库具有写入权限（通常默认已有）
- ✓ GITHUB_TOKEN 自动配置

## 📝 数据格式示例

每个谱面数据文件示例：

```json
{
  "id": "chart_id",
  "title": "谱面标题",
  "artist": "作曲者",
  "created_at": "2024-01-01T00:00:00Z",
  "updated_at": "2024-06-07T12:00:00Z",
  ...
}
```

## ⚠️ 注意事项

- **网络问题** - API 偶尔可能超时，工作流已配置重试机制
- **数据延迟** - 本仓库数据与 Phira 官方服务可能存在分钟级别的延迟
- **存储限制** - 谱面数据持续增长，注意仓库大小
- **API 限制** - 请尊重 Phira API 的使用政策，避免过度请求

## 🔍 故障排除

### 工作流执行失败

1. 查看 [Actions 日志](https://github.com/wiorigami/phiyuri/actions)
2. 检查网络连接和 API 可用性
3. 确认仓库权限配置正确

### 数据缺失

- 检查是否存在 API 限制或超时
- 重新手动触发工作流
- 查看工作流输出日志获取具体错误信息

## 📄 许可证

本项目遵循 MIT 许可证，可自由使用和修改。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📚 相关链接

- [Phira 官网](https://phira.cn/)
- [GitHub 仓库](https://github.com/wiorigami/phiyuri)

---

<div align="center">

**Made with ❤️ for Phira Community**

</div>
