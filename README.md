# 📦 Amazon Product Review Analysis System

## 📝 Project Overview

This project implements a comprehensive analysis system for Amazon product reviews using state-of-the-art Natural Language Processing (NLP) and unsupervised learning techniques. The system includes:

- **Sentiment Analysis** (using RoBERTa)  
- **Review Clustering** (using Sentence Embeddings + KMeans)  
- **Summarization of Reviews** (with T5-small model)  
- **Automated Product Comparison Articles**  
- **Interactive Web Deployment** (using Gradio)

---

## 📊 Dataset

The system uses a combination of review datasets:

- `new_data.csv` – General Amazon product reviews  
- `All_Beauty.csv` – Amazon Beauty reviews  

After cleaning and merging, the final dataset includes:

- Review text  
- Star rating (converted to sentiment)  
- Product name and category  

---

## 🧹 Data Preprocessing

Key steps:

- Map star ratings to sentiment:
  - Negative: 1–2 stars
  - Neutral: 3 stars
  - Positive: 4–5 stars
- Clean text (lowercase, punctuation removal)
- Balance dataset (equal class representation)
- Split into train/test sets (80/20)

---

## 🔍 Sentiment Analysis (RoBERTa)

### ⚙️ Model Details

- Pretrained model: `roberta-base`
- Fine-tuned for 3-class classification

**Training:**

- Epochs: 5  
- Batch size: 32  
- Learning rate: 2e-5  
- Early stopping (patience = 3)

### 📈 Performance

| Sentiment | F1 Score |
|-----------|----------|
| Negative  | ~0.90    |
| Neutral   | ~0.85    |
| Positive  | ~0.95    |

**Accuracy:** ~0.92

### 📊 Evaluation Metrics

- Accuracy  
- Precision, Recall, F1-score (per class)  
- Confusion Matrix  

### 💾 Saved Model

- `./roberta_model/` (local)  
- `/content/drive/MyDrive/roberta_model` (Google Drive)  

---

## 📚 Review Clustering

### 📌 Process

- Combined features: review text + product name + category  
- Embedding model: `MiniLM-L6-v2`  
- Clustering algorithm: KMeans (n=5)  
- Visualization: t-SNE  

### 📦 Outputs

- `kmeans_model.pkl`: Trained KMeans model  
- `cluster_names.pkl`: Cluster name mappings  
- `clustered_reviews.csv`: Labeled dataset with clusters  

### 🧠 Final Clusters

1. General Feedback  
2. Family Use & E-Reading  
3. Product Satisfaction & Family Use  
4. Battery Reviews  
5. Multi-theme  

---

## ✍️ Review Summarization

- **Model:** `t5-small`  
- For each product and sentiment, generates:
  - Summary of positive reviews  
  - Summary of negative reviews  

```python
def summarize_reviews(df, product_name, category, sentiment):
    # Extract reviews
    # Generate summary using T5-small
