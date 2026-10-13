# 严格照片面板：按需使用

仅在用户明确要求完整摄影矩形或像素保真时读取。默认融合版使用图像编辑工具，不自动运行这个流程。

保留全图原比例，向右增加画布。只有用户明确允许程序化图片处理且当前工具规则允许时，才使用已有脚本：

```bash
python scripts/protect_photo_extension.py prepare --source <source> --output <canvas.png> --manifest <layout.json>
```

检查准备画布，以它为编辑目标，仅绘制新增区域及允许的接缝。生成后执行：

```bash
python scripts/protect_photo_extension.py restore --source <source> --generated <generated> --manifest <layout.json> --output <final.png>
python scripts/protect_photo_extension.py verify --source <source> --final <final.png> --manifest <layout.json>
```

脚本默认接缝占原图宽5.5%；校验只覆盖保护列，不包含可编辑接缝，不能宣称完整原图逐像素一致。该恢复方式可能制造直线边界；严格面板模式接受这个取舍，默认融合模式不接受。

完整原图像素保真需要另行采用已获允许的全图保护与全图校验流程；无法执行时说明限制。边缘签名应独立保护，不能为了签名自动把融合版改为硬切拼贴。
