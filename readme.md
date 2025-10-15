# 🛒 E-commerce Product Recommender: Matrix Factorization (SGD) + LLM Explanations

This is a single-file, full-stack application demonstrating a modern e-commerce recommendation system that combines a sophisticated machine learning model with a Large Language Model (LLM) for personalized, explainable recommendations.

## 🚀 Project Overview

The project delivers a smart dashboard capable of recommending products and generating customized, justifiable explanations for those recommendations.

| Feature | Technology | Description |
| --- | --- | --- |
| Recommendation Model | Matrix Factorization (SGD) | A collaborative filtering technique that decomposes the user-item interaction matrix into latent feature matrices for users () and items (). This captures hidden user preferences and item characteristics. |
| Data Persistence | Firebase Firestore | Stores and retrieves mock user purchase history and interaction data persistently. |
| LLM Explanations | Gemini API (gemini-2.5-flash) | Generates natural language explanations that are grounded in the Matrix Factorization process and the user's purchase history, focusing on hidden preferences. |
| Frontend | HTML, Tailwind CSS, JavaScript | A responsive dashboard allowing user selection, history viewing, and real-time recommendation generation. |

## ⚙️ Setup and Running Locally

### Prerequisites

1.  **Web Server:** Due to the use of ES modules (type="module") and external Firebase/Gemini API calls, this file must be run from a local web server (e.g., VS Code's Live Server or Python's http.server).
2.  **API Key (If running outside of an authorized environment):** The code assumes the API\_KEY is provided at runtime. If running locally outside of the provided environment, you would need to manually insert your Gemini API key into the index.html file where const API\_KEY = ""; is defined.

### Steps to Run

1.  **Save Files:** Save index.html and products\_and\_interactions.json into a single folder.
2.  **Launch Server:** Open the folder and launch a local web server.
3.  **Access:** Navigate to the local server address (e.g., http://localhost:\[PORT\]/index.html) in your browser.
4.  **Interact:** Select a user from the dropdown and click **"Get Recommendations"**.

## 🎯 Recommendation Logic: Matrix Factorization

The core algorithm uses **Stochastic Gradient Descent (SGD)** to train a Matrix Factorization model on the implicit feedback data (purchases).

### Key Components:

1.  **User Mapping:** Maps raw user IDs (e.g., user-101) to integer indices ().
2.  **Item Mapping:** Maps product IDs (e.g., B07JW9H4J1) to integer indices ().
3.  **Latent Factors:** The model assumes that a user's preference for an item can be explained by a small number of **latent factors** (hidden dimensions, set to 2 in MF\_CONFIG).
    *   : User Latent Feature Matrix ()
    *   : Item Latent Feature Matrix ()
4.  **Prediction:** The predicted rating or preference () is the dot product of the user's vector () and the item's vector ().
5.  **Training:** SGD minimizes the error between the actual observed interaction (1 for purchased) and the predicted preference (), adjusting the vectors and iteratively.

After training, the system predicts the score for all items the user hasn't bought, and the items with the highest scores are recommended.
