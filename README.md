
# 🚧 Pothole Detection Using Traditional CV + YOLOv8 (3-Method Comparison) with Depth estimation

This project demonstrates three approaches to detect potholes from road images using **Computer Vision** and **Deep Learning**.  
The goal is to identify potholes, draw bounding boxes, and count them per image — while comparing how accuracy improves from simple CV methods to YOLOv8.

---

## 🎯 Objective
To automatically detect potholes in road surface images by:
- Identifying pothole regions  
- Marking them with bounding boxes  
- Counting the number of potholes per image  
- Comparing traditional CV techniques with YOLOv8 deep learning detection  

## 🚀 Key Project Highlights
- Implemented 3 pothole detection methods  
- Compared traditional CV vs. deep learning  
- Integrated **YOLOv8 for high-accuracy detection**  
- Added **pothole depth estimation**  
- Real-time performance suitable for smart city applications  
---

# 🧠 Method 1 — Threshold-Based Contour Extraction

This is a **basic image-processing technique** with no machine learning involved.

### 🔧 Steps:
1. Convert to grayscale  
2. Apply Gaussian blur  
3. Use **binary inverse thresholding**  
4. Apply **morphological closing**  
5. Detect contours  
6. Filter by area  
7. Draw bounding boxes  
8. Count potholes  

### ✅ Pros
- Very fast  
- Works only when potholes are clearly darker  

### ❌ Limitations
- Fails under bright light, shadows, moisture  
- Misdetects cracks, patches, and road paint  
- Misses many actual potholes  
- Not suitable for real-world deployment  

---

# 🧠 Method 2 — Texture-Enhanced Adaptive Thresholding

An improved CV method focusing on **texture differences** instead of just intensity.

### 🔧 Steps:
1. Convert to grayscale  
2. Apply Gaussian blur  
3. **Laplacian filter** → enhances edges & texture  
4. Weighted image fusion  
5. **Adaptive thresholding** (works in varying light)  
6. Morphological closing  
7. Contour detection + area filtering  
8. Draw bounding boxes & count  

### ✅ Improvements
- Handles shadows better  
- Captures texture variations  
- Detects more potholes than Method 1  

### ❌ Still not enough
- Confuses shadows with potholes  
- Road patch textures cause false positives  
- Cannot generalize to all road conditions  

---

# 🧠 Method 3 — YOLOv8 Deep Learning Object Detection (Final Approach)

Traditional CV is limited.  
So we use **YOLOv8**, a state-of-the-art deep learning model that learns pothole patterns from annotated images.

### 🔧 Steps:
1. **Dataset preparation**  
   - Labeled potholes with bounding boxes  
   - Train/test split  

2. **Model Training (Transfer Learning)**  
   - YOLOv8 learns pothole shapes, textures, edges, and patterns  

3. **Inference**  
   - Predicts bounding boxes  
   - Provides confidence scores  

4. **Visualization**  
   - Draw bounding boxes  
   - Optional: severity color coding  
     - 🟢 Small  
     - 🟡 Medium  
     - 🔴 Large  

### ⭐ Advantages
- High accuracy  
- Works under varying lighting  
- Handles shadows, blurred images, road texture variations  
- Fewer false positives  
- Real-time performance (vehicle/CCTV friendly)  

---

# 🔎 Comparison Summary

| Feature | Method-1 | Method-2 | Method-3 (YOLOv8) |
|--------|----------|----------|--------------------|
| Works in varying light | ❌ | ⚠️ Partial | ✅ |
| Detects small potholes | ❌ | ⚠️ | ✅ |
| False positives | High | Medium | Low |
| Real-time capable | ✅ | ⚠️ | ✅ |
| Real-world deployment | ❌ | ❌ | ⭐ Recommended |

**YOLOv8 outperforms both traditional methods and is the recommended approach for real-world pothole detection.**

---

🕳️ Pothole Depth Estimation (Additional Feature)

Along with pothole detection, this project also estimates the approximate depth of each pothole.
Depth estimation helps prioritize road repairs based on severity.

🔧 How Depth Estimation Works

After YOLOv8 detects potholes, each bounding box is processed.

Image features inside the region are analyzed to approximate the depth.

The depth values (in approximate units) are displayed above each pothole.

Example result:
✔ Depth: 21.957
✔ Depth: 35.785
✔ Depth: 45.896

🟡 Why Depth Matters?

Identifies dangerous potholes (deep ones)

Helps municipalities prioritize repair

Useful in autonomous vehicles, traffic surveillance, and road maintenance
