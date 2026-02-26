# Stray_Dog_Detection
## CanineSight: SOTA Behavioral Analytics Pipeline
---

## 1. My Vision: The Problem & The Solution

"I developed this project to solve a critical urban challenge: monitoring stray animal welfare and public safety. Instead of a simple detection system, I built an **end-to-end behavioral analytics pipeline** that can differentiate between a dog just resting and one engaging in 'mischievous' or aggressive activities like lunging or jumping."

## 2. My Multi-Model Architecture

"I chose a **hierarchical model approach** to balance speed and extreme precision. My system doesn't just look at a dog; it understands its posture through three distinct stages:"

* **Stage 1: Real-time Detection (YOLO11)**
"I integrated **YOLO11** as my primary detector. I chose this specific version because its spatial attention mechanisms are superior at finding dogs in cluttered environments, like under parked cars or behind street furniture. It provides me with the initial bounding boxes at high speeds."
* **Stage 2: Instance Segmentation (SAM 2.1)**
"Once I have a detection, I prompt **SAM 2.1 (Segment Anything Model)** with the YOLO bounding box. This is where my project moves beyond standard CV; I extract a pixel-perfect mask (a silhouette) of the dog. This allows me to isolate the animal from the background noise of the street."
* **Stage 3: Morphological Analysis (The Logic Layer)**
"I wrote a custom Python module to analyze these masks. By calculating the **Aspect Ratio** and **Solidity** of the dog's silhouette, my system can mathematically determine behavior. For example, if the height-to-width ratio is high, my system flags a 'Jumping' behavior."

---

## 3. My Engineering Optimizations

"To make this computationally feasible, I implemented several advanced engineering strategies:"

* **CUDA & GPU Acceleration:** "I optimized the pipeline to run on **NVIDIA GPU runtimes**. By moving the model tensors to CUDA memory, I achieved significant speedups over standard CPU processing."
* **FP16 Quantization:** "I utilized **Half-Precision (FP16)** inference. This halved the memory footprint and doubled my processing throughput without sacrificing the accuracy needed for behavior classification."
* **Frame Stride Logic:** "To handle high-resolution video from the **Kaggle 'videosdog' dataset**, I implemented a frame-striding technique. I run the heavy SAM segmentation every $n^{th}$ frame while maintaining tracking, which keeps the output smooth but fast."

---

## 4. My Data Output & Reporting

"I believe that AI is only useful if it provides actionable data. Therefore, I didn't stop at visual overlays:"

* **Visual Feedback:** "My system renders a semi-transparent colored mask over the dog's body, a bounding box with the class name, and a dynamic label showing the analyzed behavior in real-time."
* **Automated CSV Logging:** "I integrated a **Pandas-based logging system**. For every video processed, my system generates a CSV report that tracks the number of dogs, the frequency of specific behaviors, and confidence scores. This turns raw video into a structured census for urban planners or NGOs."

---

## 5. My Future Roadmap

"Moving forward, I plan to deploy this on a **Raspberry Pi 5** using a 'Light' version of my pipeline. I am also working on 'Temporal Behavior Analysis,' where the system will analyze a sequence of 10-15 frames to detect more complex actions like digging or tail-wagging patterns."

