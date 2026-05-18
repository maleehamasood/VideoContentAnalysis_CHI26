# Video Content Analysis

This repository contains the video content analysis pipeline from our CHI ’26 paper:

**Counting How the Seconds Count: Understanding Algorithm–User Interplay in TikTok via ML-driven Analysis of Video Content** — **[Paper](https://maleehamasood.github.io/content/papers/chi-226-arxiv.pdf)** | **[Slides](https://maleehamasood.github.io/content/CHI26-TikTokTalk.pdf)** | **[Talk](https://drive.google.com/file/d/1BCLF060gFvyIetVgKeds6Rendz6tmAUI/view)**

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
## Extract Video + Audio Embeddings

We use **[Video-LLaMA](https://github.com/DAMO-NLP-SG/Video-LLaMA)** to extract multimodal video and audio embeddings from TikTok videos.

### Setup

Clone Video-LLaMA and create output directories:

```bash
git clone https://github.com/DAMO-NLP-SG/Video-LLaMA.git
cd Video-LLaMA

mkdir -p embs
mkdir -p videodesc
```

### Install Conda

```bash
MINICONDA3=Miniconda3-py37_4.9.2-Linux-x86_64.sh

wget -nc https://repo.continuum.io/miniconda/$MINICONDA3 -P ~/Downloads
chmod +x ~/Downloads/$MINICONDA3
~/Downloads/$MINICONDA3 -bf

source ~/miniconda3/bin/activate base
```

### Install Dependencies

```bash
sudo apt update
sudo apt install ffmpeg
sudo apt install ubuntu-drivers-common
sudo apt install nvidia-cuda-toolkit
sudo apt install git-lfs
```

Create and activate the Video-LLaMA environment:

```bash
conda env create -f environment.yml
conda activate videollama
```

Install PyTorch:

```bash
conda install pytorch pytorch-cuda=12.1 -c pytorch -c nvidia
```

If needed, install the CUDA 11.8 PyTorch wheels explicitly:

```bash
pip install --no-cache-dir torch==2.1.2 torchvision==0.16.2 torchaudio==2.1.2 \
  --index-url https://download.pytorch.org/whl/cu118
```

### Download Video-LLaMA Checkpoints

```bash
git clone https://huggingface.co/DAMO-NLP-SG/Video-LLaMA-2-7B-Finetuned
```

### Required Code Fixes

Depending on your environment, you may need to patch `pytorchvideo`:

```bash
vim /home/maleeha2/miniconda3/envs/videollama/lib/python3.9/site-packages/pytorchvideo/transforms/augmentations.py
```

Remove `_tensor` from the imports.

### Replace Files

Replace the following files in Video-LLaMA's repository from the ones in this repository:

```text
eval_configs/video_llama_eval_withaudio.yaml
```

```text
video_llama/conversation/conversation_video.py
```

<!-- ## TikTok Videos

TikTok videos can be downloaded using the following URL format:

```text
https://www.tiktok.com/share/video/{video_id}
```

Replace `{video_id}` with the TikTok video ID.

Example:

```text
https://www.tiktok.com/share/video/7313716511095442693
``` -->

### Extract Video and Audio Embeddings

Run the embedding extraction script with:

```bash
python video2embeddings.py \
  --cfg-path eval_configs/video_llama_eval_withaudio.yaml \
  --model_type llama_v2 \
  --gpu-id 0 \
  --videoname 7313716511095442693
```

Another example:

```bash
python video2embeddings.py \
  --cfg-path eval_configs/video_llama_eval_withaudio.yaml \
  --model_type llama_v2 \
  --gpu-id 0 \
  --videoname 7636001733549870369
```

The generated embeddings are saved under:

```text
embs/
```

Video-LLaMA's response to "What is happening in the video?" is saved under:

```text
videodesc/
```

### Embedding Dimensions

For each TikTok video, the pipeline extracts both video and audio embeddings.

```text
Video embedding shape: torch.Size([1, 32, 4096])
Audio embedding shape: torch.Size([1, 8, 4096])
```

## Generate VCA Vectors

## Citation

If you use this repository or build upon this pipeline, please cite:

```bibtex
@inproceedings{masood2026counting,
  title={Counting How the Seconds Count: Understanding Algorithm--User Interplay in TikTok via ML-driven Analysis of Video Content},
  author={Masood, Maleeha and others},
  booktitle={Proceedings of the CHI Conference on Human Factors in Computing Systems},
  year={2026}
}
```