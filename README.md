# AIChef

AI 私人厨师应用。用户可以通过食材图片或文字清单搜索菜谱，并获得带评分和参考图片的食谱建议。

## 项目结构

- `app/`：FastAPI 服务、LangGraph Agent、OSS 上传签名接口及前端静态资源。
- `私厨-前端源码/`：Next.js 前端源码。
- `app/static/`：由前端源码构建并在 FastAPI 中提供的静态产物，请勿直接修改。
- `langgraph.json`：LangGraph CLI/Studio 的 Agent 入口配置。

## 本地运行

### 后端

1. 安装 [uv](https://docs.astral.sh/uv/)。
2. 复制环境变量模板并填写自己的凭据：

   ```powershell
   Copy-Item .env.example .env
   ```

3. 安装依赖并启动服务：

   ```powershell
   uv sync
   uv run uvicorn app.main:app --host 127.0.0.1 --port 8001
   ```

服务默认监听 `http://127.0.0.1:8001`。

也可以使用 LangGraph CLI 启动开发环境：

```powershell
uv run langgraph dev
```

### 前端源码

```powershell
Set-Location 私厨-前端源码
npm ci
npm run dev
```

生产静态包：

```powershell
npm run build
```

构建结果位于 `私厨-前端源码/out/`，用于更新 `app/static/`。

## 环境变量

根据 `.env.example` 配置以下服务：

- DeepSeek：主对话和食谱推荐模型。
- Tavily：网页和食谱图片搜索。
- 阿里云 OSS：食材图片上传与访问。
- LangSmith：可选的调用链追踪。

## 隐私说明

`.env`、访问凭据、SQLite 会话数据库、LangGraph 本地状态、虚拟环境和编辑器配置均已加入 `.gitignore`，不会提交到仓库。请勿提交真实密钥、用户聊天记录或上传的食材图片。
