# DCT-Pro 数字图像水印研究项目（公开演示仓库）

> DCT-Pro Image Watermarking Research Workbench — visualization, documentation, and a Windows executable demo.

本仓库公开数字图像水印研究的**交互式算法可视化**、**研究说明**与 **Windows 可执行演示程序**。研究实现的源代码不在公开范围内。

> 本仓库公开研究说明、交互式算法可视化和 Windows 可执行演示程序，研究实现源码不在公开范围内。

## Project Status

`Research prototype` · 持续迭代中（Active development）

## Overview

图像数字水印技术通过在人眼不易察觉的通道中嵌入标识信息，用于版权归属、传播溯源与内容完整性验证。本项目围绕这一方向构建了一套可运行的实验工作台，把多种经典水印方法放进同一套嵌入—攻击—提取—评估流程中进行比较。

公开内容分为三部分：

- **交互式可视化**：在浏览器中解释 DCT-Pro 算法的嵌入与提取流程、各模块的作用和相互配合；
- **Windows 可执行程序**：`v13_ex.exe`，可在本地完成水印嵌入、盲提取、攻击测试、质量评估与报告导出；
- **研究说明**：本项目当前的研究方向与实验关注点。

## Public Resources

- Interactive visualization（`index.html`，浏览器直接打开）
- Windows executable（GitHub Release 提供 `v13_ex.exe`）
- Research overview（本文件）

## What the Workbench Includes

Windows 演示程序提供四种算法模式与完整的实验闭环：

| 模式 | 说明 |
|---|---|
| `LSB` | 空间域基线方案，用于对比（对压缩、裁剪较脆弱） |
| `DCT` | 经典 DCT 中频系数比较方案，用于对比 JPEG/缩放等常见攻击 |
| `Visible` | 显性水印，用于肉眼可见的视觉对比（通常不进行盲提取） |
| `DCT-Pro` | 本项目探索的分块 DCT 增强方案，面向鲁棒性评测 |

主要能力：

- 水印**嵌入**：加载或拖拽图片、选择算法与强度、输入水印文本；
- 水印**提取**：对水印图或攻击后的图像进行盲提取并输出检测报告；
- **质量评估**：嵌入后同步输出 PSNR / SSIM，并提供差异热图查看修改分布；
- **单项攻击**：JPEG 压缩、缩放、噪声、亮度、旋转、滤波、裁剪/遮挡等；
- **批量测试**：对攻击集合统一执行并输出成功率与逐项结果；
- **组合攻击流水线**：把多个攻击原语组成多步骤破坏序列；
- **三算法对比**：同一攻击集合下对比 LSB / DCT / DCT-Pro 的提取表现；
- **报告导出**：Markdown 文本报告与图片版报告；
- **后台线程处理与进度更新**：耗时任务不阻塞界面，错误会被捕获并提示。

显水印（Visible）用于视觉对比，其行为与隐水印不同；"提取"能力以程序中实际提供的模式为准。

## DCT-Pro Research Focus

当前研究重点围绕分块 DCT 域的水印鲁棒性展开，探索内容主要包括：

- 盲提取的分块 DCT 水印；
- 将 DCT 网格相位作为主动编码或恢复维度；
- 在偏移网格上构造互补关系；
- 通过裁剪后存活方程矩阵的秩分析恢复条件；
- 面向裁剪、压缩、噪声和轻微几何变化的鲁棒性研究；
- 将多种经典水印方法放入统一实验工作台进行比较。

以上为研究方向的克制表述。本项目处于实验阶段，结论应结合具体实验条件理解，不构成对绝对鲁棒性或原创性优先权的声明。

## Interactive Visualization

浏览器可视化页面（`index.html`）用于解释 DCT-Pro 的算法流程与模块作用，包含以下模块展示：

- YUV 色彩空间与 Y 亮度通道；
- 8×8 DCT 分块；
- JND 自适应嵌入强度；
- Arnold 交织；
- DCT 系数对调制；
- tile 局部封包与重复；
- GRL 全局分散；
- m 序列同步头；
- 相位搜索；
- 轻微旋转重试；
- 多候选投票；
- CRC 校验；
- 嵌入流程与提取流程；
- 消融实验模块展示。

> 可视化页面用于解释算法流程和模块作用，不等同于完整实验代码或全部研究实现。

## Download

从本仓库的 GitHub Release 下载 Windows 演示程序：

| 项目 | 值 |
|---|---|
| Release | `v13.0` — DCT-Pro Research Workbench v13 for Windows |
| 文件名 | `v13_ex.exe` |
| 文件大小 | 172,821,504 字节（约 165 MB） |
| SHA-256 | `FA780292E6D579AE0659E9BC67A4AAA11B34B2D5698C2A11BDA6C12E31526C5C` |
| 支持系统 | Windows 10 / Windows 11 桌面端 |

下载后建议核对 SHA-256 以确认文件完整性。

## Quick Start

1. 从 GitHub Release 下载 `v13_ex.exe`；
2. 双击运行（无需安装 Python 或额外依赖，程序为独立打包）；
3. 在"嵌入"页加载或拖拽图片，选择算法与强度，输入水印文本，点击"嵌入水印"；
4. 查看 PSNR / SSIM 与差异热图，必要时"保存结果"导出水印图像；
5. 在"提取"页加载水印图或受攻击图像，选择对应算法并"提取"；
6. 在"攻击测试"页执行单项/批量/组合攻击，或运行三算法对比并导出报告。

## Evaluation Workflow

建议的实验流程：

1. 固定算法、水印文本、嵌入强度与测试图像；
2. 嵌入后记录 PSNR / SSIM；
3. 依次执行攻击并提取，记录提取文本与通过/失败状态；
4. 使用批量测试统计整体成功率；
5. 需要时导出 Markdown/图片报告归档。

嵌入与提取必须使用相同算法；图像尺寸过小会限制可嵌入的数据量。

## Current Limitations

- 这是研究与演示项目，不是商业产品；
- 鲁棒性取决于参数、图像内容和攻击类型，单次成功不代表对所有图像和攻击有效；
- PSNR、SSIM 与提取成功率应结合实验条件理解；
- 不应将其包装成不可移除或不可破解的绝对版权保护系统；
- 程序未进行商业代码签名，Windows SmartScreen 可能显示未知发布者提示。

## Source Availability

This repository provides public documentation, an interactive visualization, and a compiled Windows demo. The source code of the research implementation is not included.

本仓库公开研究说明、交互式算法可视化和 Windows 可执行演示程序，研究实现源码不在公开范围内。本仓库不是开源算法实现仓库，也不包含源码授权。

## Responsible Use

- 本项目的可视化与演示程序仅用于研究与教育目的；
- 使用者应只处理自己拥有权利或获得授权的图像；
- 不得用于伪造版权、隐蔽追踪或未经授权的数据标记；
- 发现水印图像时，应结合传播路径、授权记录和原始载体综合判断。

## Documentation

- [Release 说明](docs/RELEASE_NOTES_v13.md)
