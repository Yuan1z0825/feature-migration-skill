# 功能迁移 Skill

[English Documentation](./README.md)

一个 Claude Code 技能，通过结构化的四阶段工作流，将开源项目功能精准迁移到您的本地项目。

## 功能特点

- **深度上下文分析**：自动分析本地项目的框架、依赖和代码规范
- **开源项目调研**：使用 DeepWiki 和 GitHub API 理解开源项目架构
- **可行性评估**：识别兼容性风险，确定最小可行代码集
- **精准实现**：生成符合您项目规范的代码

## 前置要求

### 1. 安装 DeepWiki MCP 服务器

DeepWiki 提供开源项目的深度分析。安装命令：

```bash
claude mcp add -s user -t http deepwiki https://mcp.deepwiki.com/mcp
```

此命令将 DeepWiki MCP 服务器全局注册，对所有 Claude Code 会话可用。

### 2. 安装 GitHub CLI (gh)

本技能使用 `gh` 命令访问 GitHub 仓库：

**macOS:**
```bash
brew install gh
```

**Linux (Debian/Ubuntu):**
```bash
sudo apt install gh
```

**Linux (Fedora/RHEL):**
```bash
sudo dnf install gh
```

**验证安装:**
```bash
gh --version
```

**认证 GitHub CLI:**
```bash
gh auth login
```

## 安装方式

### 方法一：手动安装

1. 克隆或下载本仓库：
```bash
git clone https://github.com/your-username/feature-migration-skill.git
```

2. 将技能复制到 Claude Code 技能目录：
```bash
# 中文版
cp -r feature-migration-skill/skill_zh ~/.claude/skills/feature-migration

# 英文版
cp -r feature-migration-skill/skill_en ~/.claude/skills/feature-migration
```

### 方法二：直接下载

下载 `SKILL.md` 文件，放置到 `~/.claude/skills/feature-migration/SKILL.md`。

## 使用方法

### 触发关键词

当您提供 GitHub 链接并表达迁移意图时，技能会被触发：

- "从 https://github.com/... 迁移 XXX 功能"
- "把 https://github.com/... 集成到我的项目"
- "参考 https://github.com/... 实现 XXX"
- "基于 https://github.com/... 的实现"

### 使用示例

```
用户：我想把 https://github.com/mahmoodlab/CLAM 的注意力可视化功能
迁移到我项目的 vis_scripts 目录
```

技能将引导您完成四个阶段：

#### 阶段一：本地上下文对齐
分析您的项目结构、依赖和代码规范。

#### 阶段二：开源全貌调研
研究 CLAM 的架构，识别相关模块。

#### 阶段三：可行性分析
评估兼容性，设计迁移方案。

#### 阶段四：实现落地
生成代码并修改本地文件。

## 工作流详解

### 阶段一：本地上下文对齐

**执行内容：**
- 扫描项目目录结构
- 解析依赖文件（requirements.txt、package.json 等）
- 识别框架及其版本
- 识别代码风格规范

**输出示例：**
```markdown
## 集成环境特征

### 项目类型
机器学习研究项目

### 核心框架
- 框架: PyTorch 2.0
- Python: 3.10

### 关键模块
- feature_extractor: WSI 特征提取
- modules: MIL 模型实现
- vis_scripts: 可视化工具

### 代码风格
- 命名规范: snake_case
- 类型注解: 部分
- 文档风格: Google
```

### 阶段二：开源全貌调研

**执行内容：**
- 查询 DeepWiki 获取项目文档
- 分析 GitHub 仓库结构
- 识别核心模块及其职责
- 映射数据流和 API 接口

**输出示例：**
```markdown
## 技术全貌图谱

### 核心模块
| 模块 | 职责 | 关联度 |
|------|------|--------|
| model_utils | 注意力权重提取 | 高 |
| visualization | 热力图生成 | 高 |
| data_processing | 切片预处理 | 低 |

### 交互点
- 注意力提取: 可适配现有特征流程
- 可视化: 需要适配本地风格规范
```

### 阶段三：可行性分析

**执行内容：**
- 确定最小可行代码集
- 识别版本冲突
- 评估依赖风险
- 设计集成架构

**输出示例：**
```markdown
## MVP 代码集
| 文件 | 用途 | 必需性 |
|------|------|--------|
| attention_utils.py | 注意力提取 | 是 |
| heatmap.py | 可视化 | 是 |
| config.yaml | 配置 | 需适配 |

## 兼容性风险
| 风险 | 影响 | 缓解方案 |
|------|------|----------|
| NumPy 版本冲突 | 中 | 使用虚拟环境 |
| Matplotlib 风格 | 低 | 适配本地风格 |
```

### 阶段四：实现落地

**执行内容：**
- 深入分析源码
- 生成符合规范的代码
- 创建新文件
- 修改现有文件
- 更新配置

**输出示例：**
```markdown
## 实现完成

### 新增文件
- vis_scripts/attention_heatmap.py: 注意力可视化模块
- vis_scripts/heatmap_utils.py: 工具函数

### 修改文件
- vis_scripts/__init__.py: 添加导入

### 使用方法
from vis_scripts.attention_heatmap import generate_heatmap
heatmap = generate_heatmap(attention_weights, slide_coords)
```

## 示例案例

### 案例 1：迁移 Gradio 界面

```
用户：参考 https://github.com/gradio-app/gradio 为我的训练启动器
脚本 (web_train_launcher.py) 添加 Web 界面
```

技能将：
1. 分析您的训练启动器代码
2. 研究 Gradio 的 API 模式
3. 设计集成方案
4. 生成 Web 界面代码

### 案例 2：优化数据加载

```
用户：基于 https://github.com/pytorch/pytorch 的 DataLoader，
优化我 feature_extractor 模块的数据加载性能
```

技能将：
1. 分析当前数据加载代码
2. 研究 PyTorch DataLoader 最佳实践
3. 识别优化机会
4. 生成优化代码

### 案例 3：集成可视化功能

```
用户：把 https://github.com/mahmoodlab/CLAM 的注意力可视化
迁移到我的 vis_scripts 目录
```

技能将：
1. 分析您的可视化基础设施
2. 研究 CLAM 的可视化方法
3. 设计适配策略
4. 生成符合规范的可视化代码

### 案例 4：迁移 MIL 模型

```
用户：把 https://github.com/mahmoodlab/CLAM 的 CLAM 模型
迁移到我的项目中，我目前已有多个 MIL 模型实现
```

技能将：
1. 分析现有 MIL 模型的实现模式
2. 研究 CLAM 模型架构
3. 评估与现有代码的兼容性
4. 生成符合项目规范的模型代码

## 故障排除

### DeepWiki 不可用

如果 DeepWiki 没有索引该项目：
- 技能将跳过 DeepWiki，仅使用 GitHub API
- 您可以手动提供额外的文档

### GitHub 访问问题

如果 `gh` 命令失败：
- 检查认证状态：`gh auth status`
- 重新认证：`gh auth login`
- 验证仓库访问权限

### 大型项目

对于大型开源项目：
- 阶段二可能需要更长时间分析
- 建议明确指定特定的模块或功能范围

## 常见问题

**Q: 支持哪些编程语言？**
A: 目前主要支持 Python、JavaScript/TypeScript、Rust、Go 等主流语言的项目分析。

**Q: 迁移的代码会有许可证问题吗？**
A: 技能会在阶段三提示您注意开源项目的许可证。请确保遵守原项目的许可证要求。

**Q: 可以部分迁移吗？**
A: 可以。在阶段三确认时，您可以指定只需要特定的功能模块。

**Q: 生成的代码质量如何保证？**
A: 技能会分析您项目的代码规范，生成的代码会尽量符合您的风格。建议在阶段四后进行代码审查。

## 贡献

欢迎提交 Issue 和 Pull Request！

## 许可证

MIT License - 详见 LICENSE 文件。

## 致谢

- [DeepWiki](https://deepwiki.com) 提供开源项目分析
- [Claude Code](https://claude.ai) 提供技能框架
- 所有让这个工作流成为可能的开源项目