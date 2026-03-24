# EyesOfSmartICE - Project Memory
# v1.1 - Enriched with project context and dev rules (2026-03-25)

## 项目背景

这是 SmartICE 餐厅运营 AI 视觉巡检系统的新一代架构。

**旧架构（已 archived）：**
- `eyesofsmartice-legacy`：本地跑 YOLO 小模型 → 预处理成结构化数据存 DB → AI 查 DB（受限）
- `eyesofsmartice-realtime-legacy`：实时版本，同样是 YOLO pipeline

**新架构（本项目）：**
- AI Agent 直接调用 `get_snapshot(time, camera_ip)` 获取摄像头快照
- Agent 自主决定看哪个摄像头、什么时间、看几次，不再依赖预处理数据

## 核心工具

```python
get_snapshot(time, camera_ip)
# time: 支持历史时间戳
# camera_ip: 摄像头地址（通过映射表转换）
```

## 摄像头系统

- 摄像头有映射表，例如：ch12=A区收银台, ch13=B区迎宾岗
- 每个摄像头画面有 mask 标注桌号
- 支持多门店（不同 IP 段）

## Agent Skills 设计

Skills 定义 Agent 的巡检行为，例如：
- **脱岗检查 skill**：连续获取收银台/迎宾岗位截图 → 分析是否有人在岗
- 每个 skill 封装：要看哪些摄像头、看几次、判断逻辑

## Tech Stack

- Python（用 `uv` 管理虚拟环境）
- Supabase（通过 MCP 访问，配置在 `.mcp.json`）
- Claude API（Agent 调用 tools）

## 重要上下文

- 旧仓库已在 GitHub 上 rename + archive，本地保留为 `*-legacy` 文件夹
- 本仓库远程用 HTTPS（SSH key 未配置）：`https://github.com/JeremyDong22/EyesOfSmartICE.git`
- 部署方式：GitHub push 自动触发（不用 `zeabur deploy`）

## Dev Rules

- 用 `uv` 管理 Python 虚拟环境
- 不 commit `.env` 文件
- 不创建新 GitHub branch，除非被告知
- 不写 Markdown 文件，除非被告知
- 测试文件用完即删
