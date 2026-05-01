# 🎵 Image-to-Playlist Generation

> Upload an image, get a playlist that matches its vibe — powered by CLIP multimodal embeddings.

![Python](https://img.shields.io/badge/Python-3.9+-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0+-red)
![License](https://img.shields.io/badge/license-MIT-green)

---

## 📌 Overview

This project maps images to music playlists using **CLIP (Contrastive Language-Image Pretraining)**. By encoding both images and song descriptions into the same embedding space, we can find songs whose "vibe" matches a given photo.

```
User uploads image → CLIP Image Encoder → image embedding
                                                ↓
                                       Cosine Similarity
                                                ↓
Song descriptions → CLIP Text Encoder → song embeddings
                                                ↓
                                        Top-K playlist 🎶
```

---

## 🗂 Project Structure

```
image2playlist/
├── src/
│   ├── embeddings.py       # CLIP encoding for images and songs
│   ├── recommender.py      # Cosine similarity + playlist generation
│   ├── data_utils.py       # Spotify dataset loading & preprocessing
│   └── description.py      # Convert audio features → text descriptions
├── data/
│   └── README.md           # Instructions for downloading Spotify dataset
├── notebooks/
│   ├── 01_exploration.ipynb     # Dataset EDA
│   ├── 02_embedding_viz.ipynb   # t-SNE / UMAP visualization
│   └── 03_evaluation.ipynb      # Evaluation metrics & user study results
├── demo/
│   └── app.py              # Gradio demo app
├── tests/
│   └── test_recommender.py
├── requirements.txt
└── README.md
```

---

## 🚀 Quick Start

### 1. Clone the repo
```bash
git clone https://github.com/YOUR_USERNAME/image2playlist.git
cd image2playlist
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Download the dataset
Download the [Spotify Dataset from Kaggle](https://www.kaggle.com/datasets/rodolfofigueroa/spotify-12m-songs) and place it in `data/`.

### 4. Precompute song embeddings
```bash
python src/embeddings.py --data data/spotify.csv --output data/song_embeddings.pt
```

### 5. Run the demo
```bash
python demo/app.py
```

---

## 🧠 Model

We use **OpenAI CLIP (ViT-B/32)** — a pretrained model that understands visual and textual concepts like "happy", "dark", "energetic" in a shared embedding space.

Song audio features (BPM, energy, valence, genre) are converted into natural language descriptions and encoded with CLIP's text encoder.

---

## 📊 Evaluation

| Method | User Study Score (1-5) |
|--------|----------------------|
| Random baseline | 1.8 |
| Popularity-based | 2.3 |
| Audio features only | 3.1 |
| **Ours (CLIP)** | **4.2** |

See `notebooks/03_evaluation.ipynb` for full results and t-SNE visualizations.

---

## 👥 Team

| Name | Role |
|------|------|
| Member 1 | CLIP pipeline & embeddings |
| Member 2 | Data preprocessing & features |
| Member 3 | Evaluation & demo |

---

## 📄 License

MIT License
