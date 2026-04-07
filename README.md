# Multimodal_RAG

多模态检索增强生成系统，专注于Apache Flink技术文档的智能处理与查询。

## 项目概述

Multimodal_RAG是一个结合了多模态AI和检索增强生成技术的智能系统，专门用于处理和查询Apache Flink相关的技术文档。该系统能够：

- 解析PDF文档并提取文本和图片内容
- 构建多模态知识库（文本+图片）
- 利用向量数据库进行高效检索
- 结合多模态大语言模型生成准确的回答
- 提供直观的Web界面进行操作

## 核心功能

1. **PDF文档处理**：自动解析PDF文件，提取文本和图片内容
2. **多模态知识库**：将文本和图片向量化存储到Milvus向量数据库
3. **智能检索**：根据用户查询智能检索相关内容
4. **多模态回答**：结合文本和图片信息生成综合回答
5. **工作流管理**：基于LangGraph的复杂工作流处理
6. **人工审批**：关键节点支持人工干预和审批

## 项目结构

```
Multimodal_RAG/
├── main.py                 # 主应用程序，提供Gradio界面
├── my_llm.py               # 多模态LLM配置
├── dots_ocr/               # PDF解析和OCR模块
│   ├── parser.py           # PDF解析器
│   ├── inference.py        # OCR推理
│   └── utils/              # OCR工具函数
├── milvus_db/              # Milvus数据库操作
│   ├── db_operator.py      # 数据库操作
│   ├── collections_operator.py # 集合操作
│   └── db_retriever.py     # 数据检索
├── graph/                  # LangGraph工作流
│   ├── workflow.py         # 工作流定义
│   ├── workflow_gradio.py  # Gradio工作流界面
│   ├── my_state.py         # 状态定义
│   └── search_node.py      # 检索节点
├── evaluate/               # 评估模块
├── splitters/              # 文档分割器
├── utils/                  # 通用工具函数
└── output/                 # 输出目录
```

## 技术栈

- **Python**：主要开发语言
- **LangChain**：构建LLM应用
- **Milvus**：向量数据库
- **Gradio**：Web界面
- **多模态LLM**：处理文本和图片
- **LangGraph**：工作流管理

## 安装指南

### 前置依赖

- Python 3.8+
- Milvus向量数据库
- 多模态LLM API访问权限

### 安装步骤

1. 克隆项目

```bash
git clone <repository-url>
cd Multimodal_RAG
```

2. 安装依赖

```bash
pip install -r requirements.txt
```

3. 配置Milvus连接

在`milvus_db/collections_operator.py`中配置Milvus连接信息。

4. 配置LLM API

在`my_llm.py`中配置多模态LLM的API访问信息。

## 使用说明

### 1. 构建知识库

1. 运行主应用：

```bash
python main.py
```

2. 在Web界面上传PDF文件
3. 点击"解析PDF"按钮处理文档
4. 查看解析结果，确认无误后点击"存入知识库"

### 2. 智能查询

1. 运行工作流：

```bash
python graph/workflow.py
```

2. 输入查询内容（文本或图片）
3. 系统会自动检索相关内容并生成回答
4. 对于重要回答，系统会请求人工审批

### 3. 多模态查询

- 文本查询：直接输入问题
- 图片查询：输入图片路径
- 混合查询：使用`&`分隔文本和图片路径，例如：`如何使用Flink & path/to/image.jpg`

## 工作流程

1. **输入处理**：分析用户输入类型（文本/图片/混合）
2. **检索决策**：决定是否需要检索知识库
3. **知识检索**：从Milvus数据库检索相关内容
4. **生成回答**：结合检索内容生成回答
5. **评估回答**：评估回答质量
6. **人工审批**：重要回答需要人工审批
7. **网络搜索**：必要时进行网络搜索补充信息
8. **结果存储**：将对话结果存入上下文数据库

## 配置说明

### 环境变量

- `MILVUS_HOST`：Milvus服务器地址
- `MILVUS_PORT`：Milvus服务器端口
- `LLM_API_KEY`：多模态LLM API密钥

### 配置文件

- `my_llm.py`：LLM配置
- `milvus_db/collections_operator.py`：Milvus配置
- `utils/embeddings_utils.py`：嵌入模型配置

## 性能优化

1. **批量处理**：PDF解析和向量化采用批量处理
2. **并行计算**：使用多线程加速PDF解析
3. **缓存机制**：缓存检索结果提高响应速度
4. **异步操作**：使用异步IO提高系统吞吐量

## 应用场景

- **技术文档查询**：快速检索Apache Flink相关技术文档
- **知识管理**：构建和管理技术知识库
- **智能客服**：提供技术支持和问答服务
- **教育培训**：辅助学习和理解技术概念

## 开发指南

### 扩展功能

1. **支持更多文档格式**：添加对Word、Excel等格式的支持
2. **增强OCR能力**：提高图片文本识别精度
3. **多语言支持**：添加对多语言文档的处理能力
4. **自定义工作流**：根据特定需求定制工作流程



