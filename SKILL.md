# uptime_kuma_api_v2

Uptime Kuma HTTP Bridge - 暴露 Uptime Kuma 为简单的 REST-like API，无需 Socket.IO 客户端即可管理监控、标签和状态检查。

## 功能

- 完整的监控管理：创建、编辑、删除、暂停、恢复
- 标签支持：添加、删除、替换监控标签，动态创建新标签自定义颜色
- Bearer token 认证
- 支持 2FA/TOTP
- 持久化连接：自动重连
- 零额外依赖基础使用，pyotp 自动安装（如需 2FA）

## 依赖安装

```bash
pip install "python-socketio[client]" websocket-client pyotp
```

## 使用方式

1. 复制 `.env.example` 为 `.env` 并修改配置：

```env
BRIDGE_HOST=127.0.0.1
BRIDGE_PORT=9911
BRIDGE_TOKEN=your-secret-token

KUMA_URL=http://your-kuma-server:3001
KUMA_USERNAME=admin
KUMA_PASSWORD=your-kuma-password

# 仅当开启 2FA 时需要
KUMA_2FA_SECRET=

# Socket.IO 调用超时（默认 60 秒）
KUMA_TIMEOUT=60
```

2. 启动服务：

```bash
python uptime_kuma.py
```

## API 端点

所有端点接受并返回 `application/json`，成功返回 `{"ok": true}`，失败返回 `{"ok": false, "error": "..."}`

- `GET /health` - 健康检查
- `POST /monitors/list` - 列出所有监控
- `POST /monitors/find` - 通过 URL 查找监控
- `POST /monitors/add` - 添加监控
- `POST /monitors/edit` - 编辑监控
- `POST /monitors/delete` - 删除监控
- `POST /monitors/pause` - 暂停监控
- `POST /monitors/resume` - 恢复监控
- `POST /monitors/status` - 获取监控状态/心跳
- `POST /tags/list` - 列出所有标签
- `POST /monitors/tags/set` - 添加标签到监控
- `POST /monitors/tags/delete` - 从监控删除标签
- `POST /monitors/sniff` - 调试，捕获添加监控的原始 payload

更多使用示例和细节请参考 [原项目 README](https://github.com/pr1ncey1987/uptime-kuma-api-v2)

## 作为技能使用

本技能封装了 uptime-kuma-api-v2 桥接服务，可以通过 copaw 技能直接调用管理 Uptime Kuma。
