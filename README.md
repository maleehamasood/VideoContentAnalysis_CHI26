# Video Content Analysis

This repository contains the video content analysis pipeline from our CHI ’26 paper:

**Counting How the Seconds Count: Understanding Algorithm–User Interplay in TikTok via ML-driven Analysis of Video Content**

**[Paper](https://maleehamasood.github.io/content/papers/chi-226-arxiv.pdf)**  
**[Slides](https://maleehamasood.github.io/content/CHI26-TikTokTalk.pdf)**  
**[Talk](https://drive.google.com/file/d/1BCLF060gFvyIetVgKeds6Rendz6tmAUI/view)**

---

## Overview

```text
TikTok Videos
      ↓
Extract Video + Audio Embeddings
      ↓
Generate VCA Vectors
      ↓
Downstream Analysis
```

The generated **Video Content Analysis (VCA)** vectors can be used for:

- Content clustering
- Feed diversity analysis
- Temporal behavior analysis
- Similarity search
- User-interest modeling
- Recommendation system analysis

---

## TikTok Videos

TikTok videos can be downloaded using the following URL format:

```text
https://www.tiktok.com/share/video/{video_id}
```

Replace `{video_id}` with a valid 19 digit TikTok video ID.

Example:

```text
https://www.tiktok.com/share/video/1234567890123456789
```

---

## Extract Video and Audio Embeddings

We use **[Video-LLaMA](https://github.com/DAMO-NLP-SG/Video-LLaMA)** to extract multimodal video and audio embeddings from TikTok videos.

The extracted embeddings are combined to generate **VCA vectors**, which serve as compact semantic representations of video content for downstream analysis.

---

## Citation

If you use this repository or build upon this pipeline, please cite:

```bibtex
@inproceedings{10.1145/3772318.3790311,
author = {Masood, Maleeha and Kannan, Shreya and Liu, Zikun and Vasisht, Deepak and Gupta, Indranil},
title = {Counting How the Seconds Count: Understanding TikTok Behavior via ML-driven Analysis of Video Content},
url = {https://doi.org/10.1145/3772318.3790311},
booktitle = {Proceedings of the 2026 CHI Conference on Human Factors in Computing Systems},
series = {CHI '26}
}
```