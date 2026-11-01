# YOLO 与 DeepSeek/Qwen 大语言模型水稻病虫害检测系统   | 水稻病虫害 YOLO DeepSeek 智慧农业 病害识别 9206期

## 系统概述

本系统基于 **YOLO 目标检测模型**与 **DeepSeek/Qwen 大语言模型**，融合 **Pytorch、SpringBoot、Flask、Vue3、MySQL** 等技术，构建了一套完整的**水稻病虫害识别与智能分析平台**。系统支持批量检测、图片检测、视频检测、摄像头检测四种方式，适配智慧农业、植保监测及农技推广等场景。
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/396cf19d306049b68ab5d4b508a5527b.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/24ebad79881c42f6a914c4205257e887.png)

## 系统核心信息

| 项目 | 详细说明 |
| :--- | :--- |
| **检测类别** | 共 **8** 类：`细菌枯病`、`褐斑病`、`健康`、`叶瘟病`、`纹枯病`、`窄条斑病`、`穗颈瘟`、`稻铁甲虫` |
| **核心技术** | YOLO + DeepSeek/Qwen + Pytorch + Flask + SpringBoot + Vue3 |
| **检测模式** | 批量检测、图片检测、视频检测、摄像头实时检测 |
| **系统架构** | 前后端分离（Vue3 + SpringBoot + Flask + MySQL） |
| **应用价值** | 1. **病害预警**：支撑水稻主要病害的早期自动化筛查，辅助精准施药。<br>2. **虫情监测**：识别稻铁甲虫等害虫，辅助虫情预报与防治决策。<br>3. **智能分析**：结合大语言模型生成病害分析与防治建议。<br>4. **智慧农业**：为水稻种植管理提供视觉识别与决策支持。 |


![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/d6581969d08e460a8e86f0cc73c6d198.png)
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/fda4ee1795fb46d39e0d551e4e3041d1.png)

## 完整类别列表（共8类）

| 序号 | 中文类别名称 | 类别说明 |
|:---:|:---|:---|
| 1 | 细菌枯病 | 细菌性病害，叶片枯萎 |
| 2 | 褐斑病 | 真菌性病害，叶片褐色斑点 |
| 3 | 健康 | 无病害症状的正常水稻 |
| 4 | 叶瘟病 | 稻瘟病的叶部表现 |
| 5 | 纹枯病 | 真菌性病害，叶鞘和叶片出现云纹状病斑 |
| 6 | 窄条斑病 | 细菌性病害，叶片出现窄条状斑 |
| 7 | 穗颈瘟 | 稻瘟病的穗颈部位表现 |
| 8 | 稻铁甲虫 | 水稻害虫，成虫啃食叶片 |


![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/e1f399f8aac24c33bae87e8c669e9ed0.png)

## 技术栈

| 层次 | 技术选型 |
| :--- | :--- |
| **深度学习** | YOLO、Pytorch |
| **算法服务** | Flask |
| **业务后端** | SpringBoot、MyBatis-Plus |
| **前端** | Vue3、Echarts、TypeScript、Element-Plus、Axios |
| **数据库** | MySQL |
| **AI 分析** | DeepSeek、Qwen |

## 系统功能

**1. 用户管理**
- 用户登录、注册
- 分用户管理：管理员可查看所有记录，普通用户只能看自己的记录
- 个人中心：查看与修改个人信息

**2. 多模态检测支持**
- **图片检测**：单张图片上传识别
- **批量检测**：支持上传文件夹批量检测
- **视频检测**：上传视频，逐帧分析并输出标注视频
- **摄像头实时检测**：连接摄像头，实时输出检测结果

**3. 检测结果可视化**
- 检测结果可视化展示
- 病害类别与置信度展示
- 检测结果可导出 PDF

**4. AI 智能建议**
- 结合 DeepSeek、Qwen 等大模型，给出相关病害分析与防治建议
- 提供详细检测报告

**5. 界面个性化**
- 界面简洁美观
- 支持主题色修改、布局样式修改、组件大小修改等

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/56be7454fce44794a87345644fe179cd.png)

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/3c1cdaccc54743a79977b627755f1cbe.png)

## 交付内容

1. **整理好的 YOLO 格式数据集**
2. **详细的系统部署教程**
3. **实时视频、摄像头、图片检测**
4. **代码简洁，有注释**
5. **提供训练好的 YOLO 权重**




## 快速开始（代码示例）

**1. 数据集配置文件 (`data.yaml`)**
```yaml
train: ./dataset/images/train
val: ./dataset/images/val
nc: 8
names: ['细菌枯病', '褐斑病', '健康', '叶瘟病', '纹枯病', '窄条斑病', '穗颈瘟', '稻铁甲虫']
```

**2. YOLO 训练代码**
```python
from ultralytics import YOLO

model = YOLO('yolov8m.pt')
model.train(
    data='data.yaml',
    epochs=100,
    imgsz=640,
    batch=16,
    device=0
)
```

**3. Flask 推理与 AI 分析服务**
```python
from flask import Flask, request, jsonify
from ultralytics import YOLO
import cv2
import numpy as np

app = Flask(__name__)
model = YOLO('runs/detect/train/weights/best.pt')

@app.route('/detect', methods=['POST'])
def detect():
    file = request.files['image']
    img = cv2.imdecode(np.frombuffer(file.read(), np.uint8), cv2.IMREAD_COLOR)
    results = model(img)
    detections = []
    for box in results[0].boxes:
        detections.append({
            'class': model.names[int(box.cls[0])],
            'confidence': float(box.conf[0]),
            'bbox': box.xyxy[0].tolist()
        })
    # 调用 DeepSeek/Qwen 生成病害分析与防治建议
    ai_suggestion = analyze_with_llm(detections)
    return jsonify({'detections': detections, 'suggestion': ai_suggestion})

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

**4. Vue3 前端检测页面**
```vue
<template>
  <div class="detector-container">
    <el-upload action="/api/detection/image" :on-success="handleSuccess">
      <el-button type="primary">上传图片</el-button>
    </el-upload>
    <div v-if="resultImage" class="result-area">
      <img :src="resultImage" alt="Detection Result" />
      <el-table :data="detections" border>
        <el-table-column prop="class" label="病害类别" />
        <el-table-column prop="confidence" label="置信度" />
      </el-table>
      <el-button @click="exportPDF">导出 PDF 报告</el-button>
    </div>
  </div>
</template>
```

## 标签
`水稻病虫害` `YOLO` `DeepSeek` `智慧农业` `病害识别` `目标检测` `深度学习` `计算机视觉`
