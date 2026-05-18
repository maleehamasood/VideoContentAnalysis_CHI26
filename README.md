# Video Content Analysis

This repository contains the video content analysis pipeline from our CHI ’26 paper:

**Counting How the Seconds Count: Understanding Algorithm-User Interplay in TikTok via ML-driven Analysis of Video Content**

**[Paper](https://maleehamasood.github.io/content/papers/chi-226-arxiv.pdf)**
**[Slides](https://maleehamasood.github.io/content/CHI26-TikTokTalk.pdf)**
**[Talk](https://drive.google.com/file/d/1BCLF060gFvyIetVgKeds6Rendz6tmAUI/view)**

## Video Content Analysis Pipeline

```text
TikTok Videos -> Extract Video and Audio Embeddings -> VCA vectors that can be used for analysis
```

## TikTok Videos

TikTok videos can be downloaded using the following URL format:

```text
https://www.tiktok.com/share/video/{video_id}
```

## Extract Video and Audio Embeddings

We use **[Video-LLaMA](https://github.com/DAMO-NLP-SG/Video-LLaMA)** to extract video and audio embeddings. 
