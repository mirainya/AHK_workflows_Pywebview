# 织流 FlowWeaver

> 可视化桌面自动化引擎 — 拖拽编排流程，所见即所得。

![Python 3.10+](https://img.shields.io/badge/Python-3.10+-3776ab?logo=python&logoColor=white)
![Windows](https://img.shields.io/badge/Windows-0078D6?logo=windows&logoColor=white)
![React](https://img.shields.io/badge/React-18-61dafb?logo=react&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)

## 它能做什么？

织流是一个面向 Windows 的桌面自动化工具。通过节点图编辑器拖拽连线，把键鼠操作、图像识别、条件判断、循环逻辑编排成完整的自动化流程，绑定热键一键触发。

**典型场景**：游戏宏、重复性办公操作、UI 自动化测试、个人效率脚本。

## 核心能力

| 模块 | 说明 |
|------|------|
| 节点图编辑器 | 基于 React Flow 的可视化流程编排，支持分支、循环、嵌套 |
| 图像识别 | OpenCV 模板匹配 + 异步后台监控，结果自动写入变量 |
| 键鼠控制 | 单键/组合键/序列、鼠标点击/拖拽/滚轮，支持坐标和变量两种模式 |
| 像素检测 | 单点/多点/区域颜色检测、HSV 色域匹配、指纹匹配 |
| 条件 & 循环 | if/else 分支、变量条件判断、计数循环/条件循环 |
| 热键系统 | 全局热键注册，三种运行模式（单次 / N次 / 开关循环） |
| 变量系统 | 局部变量 + 跨流程共享变量，识图结果自动存储 |

## 快速开始

### 环境要求

- Python 3.10+
- Node.js 18+
- Windows 10/11

### 安装

```bash
# 克隆项目
git clone https://github.com/mirainya/AHK_workflows_Pywebview.git
cd AHK_workflows_Pywebview

# Python 依赖（推荐虚拟环境）
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt

# 前端依赖
cd app/ui && npm install && npm run build && cd ../..
```

### 运行

```bash
.venv\Scripts\python main.py
```

### 打包

```bash
# 前端构建
cd app/ui && npm run build && cd ../..

# PyInstaller 打包
.venv\Scripts\pyinstaller build.spec

# 复制资源
xcopy /E /I /Y data dist\LuoqiAssistant\data
xcopy /E /I /Y assets dist\LuoqiAssistant\assets
```

## 支持的节点类型

| 分类 | 节点 | 用途 |
|------|------|------|
| 键盘 | key_tap / key_sequence / key_hold | 按键、组合键序列、长按 |
| 鼠标 | click_point / mouse_move / mouse_drag / mouse_scroll / mouse_hold | 点击、移动、拖拽、滚轮、长按 |
| 视觉 | detect_image / detect_color / check_pixels / check_region_color / detect_color_region / match_fingerprint | 模板匹配、颜色检测、像素校验、区域色检、HSV匹配、指纹匹配 |
| 逻辑 | if_var_found / if_condition / loop | 变量存在判断、条件分支、循环 |
| 数据 | set_variable / set_variable_state / type_text | 设置变量、修改状态、文本输入 |
| 控制 | delay / log / call_workflow | 延时、日志、调用子流程 |

## 项目结构

```
织流 FlowWeaver
├── main.py                  # 入口
├── app/
│   ├── application.py       # 应用编排
│   ├── api.py               # pywebview ↔ 前端桥接
│   ├── core/
│   │   ├── executor.py      # 流程执行引擎
│   │   ├── hotkeys.py       # 全局热键
│   │   ├── workflows.py     # 工作流管理
│   │   └── handlers/        # 各类步骤处理器
│   ├── services/
│   │   ├── vision.py        # 图像识别
│   │   ├── async_vision.py  # 异步后台识图
│   │   └── input_controller.py
│   └── ui/                  # React + TypeScript 前端
│       └── src/
│           ├── components/node-editor/  # 节点图编辑器
│           ├── stores/                  # Zustand 状态管理
│           └── models/                  # 数据模型
├── assets/templates/        # 图像模板
├── data/config.json         # 运行时配置
└── requirements.txt
```

## 技术栈

**后端**：Python · pywebview · OpenCV · Pillow · MSS · keyboard

**前端**：React 18 · TypeScript · @xyflow/react · Zustand · Vite

## License

MIT
