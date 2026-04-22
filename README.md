# ComfyUI_GPTImage2

通过云端 API 集成 gpt-image-2 图像生成模型的 ComfyUI 节点。

## 安装

1. 将文件夹复制到 `ComfyUI/custom_nodes/` 目录
2. 安装依赖：`pip install -r requirements.txt`
3. 编辑 `config.json` 填入 API 地址和密钥
4. 重启 ComfyUI

## 节点

### 文生图 (Text2Img)

根据文本提示词生成图像。

**参数：**

| 参数 | 选项 | 默认值 | 说明 |
|------|------|--------|------|
| prompt | 字符串 | — | 图像描述 |
| model | gpt-image-2, gpt-image-1.5, gpt-image-1 | gpt-image-2 | 模型 |
| quality | low, medium, high, auto | medium | 质量 |
| size | 1024x1024, 1536x1024, 1024x1536, auto | 1024x1024 | 分辨率 |
| n | 1-10 | 1 | 生成数量 |
| seed | 整数 | -1 | 随机种子 |
| output_format | png, jpeg, webp | png | 输出格式 |

### 图生图 (Img2Img)

在文本引导下转换输入图像。

**参数：**

| 参数 | 选项 | 默认值 | 说明 |
|------|------|--------|------|
| image1 | IMAGE | — | 输入图像（必填） |
| prompt | 字符串 | — | 转换指令（必填） |
| model | gpt-image-2, gpt-image-1.5, gpt-image-1 | gpt-image-2 | 模型 |
| input_fidelity | low, high | high | 保持原图程度 |
| quality | low, medium, high, auto | medium | 质量 |
| size | 1024x1024, 1536x1024, 1024x1536, auto | 1024x1024 | 分辨率 |
| n | 1-10 | 1 | 生成数量 |
| seed | 整数 | -1 | 随机种子 |
| output_format | png, jpeg, webp | png | 输出格式 |
| image2-image5 | IMAGE | — | 可选附加图像 |

## 配置

编辑 `config.json`：

```json
{
  "base_url": "https://api.bltcy.ai/v1",
  "api_key": "你的_api_key"
}
```

## 常见问题

- **生成慢**：降低 quality 或减小 size，网络不稳定也会影响速度
- **无图像返回**：检查 api_key 和账户额度
- **超时**：可调高 nodes.py 中的 timeout 参数（默认 120 秒）
