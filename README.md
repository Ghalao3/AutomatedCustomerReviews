# Amazon Product Review Analysis Project

## 1. Project Description

### **Project Overview:**
This project is a web-based application designed to analyze Amazon product reviews using machine learning techniques such as sentiment classification, product category clustering, and review summarization. The goal is to assist marketing teams and decision-makers by providing instant insights into how products are perceived by customers, common issues, and product performance within different categories.

### **Main Objectives:**
- Classify customer reviews as Positive, Neutral, or Negative.
- Cluster products into categories.
- Generate article-like summaries for each product or category.

---

## 2. Datasets and Preprocessing

### **A. Datasets Used:**
1. **clustered_reviews.csv**: Contains Amazon reviews with precomputed clustering labels, product names, and categories.
2. **balanced_reviews_dataset.csv**: A balanced dataset to support effective sentiment classification.

### **B. Preprocessing Steps:**
1. Loaded both datasets and checked for missing values.
2. Renamed inconsistent columns for merging (e.g., `reviews.text` to `text`, `product_name` to `name`).
3. Created a unified dataset with consistent column names: `name`, `text`, `categories`, `cluster_name`.
4. Cleaned the text fields by removing extra commas, line breaks, and duplicate reviews.
5. Limited the number of reviews processed per product to speed up model inference.

---

## 3. Task Approach

### **A. Sentiment Classification:**
- **Model Used**: `roberta_model` (fine-tuned for text classification)
- **Purpose**: Classifies each review as Positive, Neutral, or Negative.
- **Implementation**:
  - Tokenized review text using `AutoTokenizer`.
  - Passed input to `AutoModelForSequenceClassification`.
  - Used model logits to determine the predicted sentiment label.

### **B. Product Category Clustering:**
- **Precomputed Offline**: Using KMeans on sentence embeddings.
- **Cluster Labels**: Mapped to descriptive categories (e.g., Ebook Readers, Batteries, Accessories).
- **Usage**: Enables users to search by category or view group-level insights.

### **C. Review Summarization:**
- **Model Used**: `t5_small` (pretrained summarization model)
- **Purpose**: Generates brief, coherent summaries of product feedback.
- **Steps**:
  - Cleaned and deduplicated review text.
  - Limited to 3 representative reviews per product.
  - Formatted a prompt: "Summarize reviews for 'Product X'..."
  - Used Hugging Face pipeline to generate summaries.
  - Repeated for top 3 products in the category and one worst-rated product.

---

## 4. Web Application (User Interface)

- **Framework**: Gradio (Blocks)
- **Theme**: Soft layout with Amazon branding
- **https://drive.google.com/drive/folders/1_tzKFgf_JAs3VyfMJCb6eFmAFZQzryci?usp=drive_link**

### **Layout Features:**
- Amazon logo, large headline, and call-to-action.
- Input field for product/category search.
- Accordion-style result display for a clean user experience.
- Output boxes for matched product, category, sentiment stats, and AI-generated summaries.

### **Styling**:
- Integrated a TailwindCSS-like appearance.
- Used Gradio Markdown and column components for layout.
- Icons and color highlights enhance readability and engagement.

---

## 5. Final Features Summary:
- 🔍 **Search by product or category name**
- 🧾 **Return the matched product and cluster category**
- 📊 **Visualize the sentiment distribution from classified reviews**
- 📝 **Generate a summary with**:
  - Top 3 products in category (with complaint count)
  - AI-generated summary for each product
  - Worst-rated product with generated summary
