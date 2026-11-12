<p align="center">
  <img src="logo/light.png" alt="DreamTo" height="48">
</p>

# DreamTo API 文档

[English](#english)

DreamTo 开放平台的 API 对接文档。通过统一的 HTTP 接口调用：

- **Seedance 2.0 视频生成**：文生视频、图生视频、首尾帧、多图参考、视频编辑 / 延长、参考音频、联网搜索增强
- **Seedance 素材库**：长期保存参考素材，在任务中通过 `asset://<素材Id>` 反复引用
- **任务回调**：任务完成后主动推送结果，支持 HMAC-SHA256 签名校验

每个接口都有完整的参数说明（中英文、逐个取值解释）和 11 个场景示例，可以在文档页面上直接 **Try it** 在线调试。

**Base URL**：`https://api.dreamto.ai`

## 快速开始

1. 登录 [DreamTo](https://www.dreamto.ai) 控制台，在 **API Key** 页面创建 API Key。
2. 创建视频生成任务：

   ```bash
   curl -X POST "https://api.dreamto.ai/api/v3/contents/generations/tasks" \
     -H "Authorization: Bearer $DREAMTO_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{
       "model": "seedance-2.0",
       "content": [
         { "type": "text", "text": "一只橘猫在阳光下的窗台上伸懒腰，慢镜头" }
       ],
       "ratio": "16:9",
       "duration": 5,
       "resolution": "720p"
     }'
   ```

   返回 `{"id": "task_...", "request_id": "req_..."}`。

3. 查询结果，`status` 为 `succeeded` 时从 `content.video_url` 下载视频：

   ```bash
   curl "https://api.dreamto.ai/api/v3/contents/generations/tasks/task_xxx" \
     -H "Authorization: Bearer $DREAMTO_API_KEY"
   ```

   也可以在创建任务时传 `callback_url`，由平台主动推送结果。

## 文档目录

| 内容 | 中文 | English |
|---|---|---|
| 简介与快速开始 | [index.mdx](index.mdx) | [en/index.mdx](en/index.mdx) |
| 认证 | [authentication.mdx](authentication.mdx) | [en/authentication.mdx](en/authentication.mdx) |
| 错误码 | [errors.mdx](errors.mdx) | [en/errors.mdx](en/errors.mdx) |
| Seedance 2.0 视频生成 | [video/seedance-2-0.mdx](video/seedance-2-0.mdx) | [en/video/seedance-2-0.mdx](en/video/seedance-2-0.mdx) |
| 场景示例 | [video/seedance-2-0/scenarios/](video/seedance-2-0/scenarios/) | [en/video/seedance-2-0/scenarios/](en/video/seedance-2-0/scenarios/) |
| Seedance 素材库 | [assets/seedance-asset-library.mdx](assets/seedance-asset-library.mdx) | [en/assets/seedance-asset-library.mdx](en/assets/seedance-asset-library.mdx) |
| 任务回调 | [webhooks/task-callback.mdx](webhooks/task-callback.mdx) | [en/webhooks/task-callback.mdx](en/webhooks/task-callback.mdx) |
| OpenAPI 定义 | [openapi/zh.json](openapi/zh.json) | [openapi/en.json](openapi/en.json) |

`openapi/*.json` 是标准 OpenAPI 3.1 文件，可以直接导入 Postman、Apifox 等工具，或用来生成 SDK。

## 反馈

发现文档错误或有接入问题，欢迎提 [Issue](https://github.com/dreamtoai/dreamtoai-docs/issues)。排查接口问题时请附上响应中的 `request_id`，**不要贴出 API Key**。

OpenAPI 定义和场景示例由 DreamTo 服务端代码自动生成，相关修改请通过 Issue 反馈，不接受直接修改这些文件的 PR。

## 本地预览

```bash
npm i -g mint
mint dev
```

打开 http://localhost:3000 。

---

<a id="english"></a>

# DreamTo API docs

API documentation for the DreamTo platform. One HTTP API for:

- **Seedance 2.0 video generation**: text-to-video, image-to-video, first/last frame, multi-image reference, video edit / extend, reference audio, web search
- **Seedance asset library**: store reference material and reuse it in tasks via `asset://<asset Id>`
- **Task callbacks**: results pushed to your server when a task finishes, signed with HMAC-SHA256

Every endpoint documents each parameter and each allowed value (in Chinese and English), with 11 scenario examples you can run with **Try it** on the docs page.

**Base URL**: `https://api.dreamto.ai`

## Quick start

1. Sign in to the [DreamTo](https://www.dreamto.ai) console and create an API key on the **API Key** page.
2. Create a video task:

   ```bash
   curl -X POST "https://api.dreamto.ai/api/v3/contents/generations/tasks" \
     -H "Authorization: Bearer $DREAMTO_API_KEY" \
     -H "Content-Type: application/json" \
     -d '{
       "model": "seedance-2.0",
       "content": [
         { "type": "text", "text": "An orange cat stretches on a sunny windowsill, slow motion" }
       ],
       "ratio": "16:9",
       "duration": 5,
       "resolution": "720p"
     }'
   ```

   The response is `{"id": "task_...", "request_id": "req_..."}`.

3. Poll the task. When `status` is `succeeded`, download the video from `content.video_url`:

   ```bash
   curl "https://api.dreamto.ai/api/v3/contents/generations/tasks/task_xxx" \
     -H "Authorization: Bearer $DREAMTO_API_KEY"
   ```

   Or pass `callback_url` when creating the task to have the result pushed to you.

English pages live under [`en/`](en/). The OpenAPI 3.1 definitions in [`openapi/`](openapi/) can be imported into Postman and similar tools or used to generate SDKs.

## Feedback

Found a mistake or need help integrating? Open an [issue](https://github.com/dreamtoai/dreamtoai-docs/issues). Include the `request_id` from the response, and **never post your API key**.

The OpenAPI definitions and scenario pages are generated from DreamTo's server code, so please report changes to them as issues rather than PRs that edit those files.
