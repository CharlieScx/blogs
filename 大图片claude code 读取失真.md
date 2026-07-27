1.大图片claude code 读取失真
超大原图 → Claude Read 自行压缩 → 压缩参数不可控 → 小字失真

超大原图 → Agent 按明确规则预压缩 → 写入本地文件
         → Claude Read 读取受控图片 → 尽量避免二次压缩

         ```mermaid
flowchart LR
    A["resource_link 图片 URL"] --> B["acp-agent 下载为 Buffer"]
    B --> C["image-optimizer 分析尺寸和格式"]
    C --> D{"是否需要优化"}
    D -->|"不需要"| E["原图写入 userFiles"]
    D -->|"需要"| F["缩放 + JPEG 重编码"]
    D -->|"异常"| G["回退并保存原图"]
    F --> H["返回优化后文件路径"]
    E --> H
    G --> H
    H --> I["拼接图片路径提示词"]
    I --> J["Claude CLI 使用 Read 读取"]
```

