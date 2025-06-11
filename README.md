# 🃏 JesterMate: User-User Collaborative Joke Recommender

**JesterMate** is a user-user collaborative filtering system designed to recommend jokes based on user similarity using the Jester Dataset (2.3M+ ratings). It applies fundamental recommender system concepts to deliver personalized humor suggestions and includes performance comparison with a baseline random recommender.

---

## 🔍 Features

- 👤 User-User Collaborative Filtering using Cosine Similarity  
- 🎯 Top-K Similar Users for rating prediction (tunable `k`)  
- 📊 MAE Evaluation for model comparison  
- 🎲 Random Baseline for performance benchmarking  
- 📈 Top-2K Similar Users with similarity scores  
- 😄 Top-N Joke Recommendations for any user  
- 🧼 Preprocessing: Handling missing values, filtering active users  

---

## 🧠 Dataset

- **Source**: [Jester Dataset](https://goldberg.berkeley.edu/jester-data/)  
- **Variant Used**: Dataset 3 (2.3 million joke ratings)  
- **Ratings Range**: -10 (worst) to +10 (best)  
- **Unrated Jokes**: Represented as `99`, replaced with `NaN` during preprocessing.  

---

## ⚙️ Architecture Overview

          ┌──────────────────────────┐
          │   Raw Joke Ratings CSV   │
          └────────────┬─────────────┘
                       ↓
       ┌────────────────────────────────────┐
       │   Filter Active Users (≥ 80 jokes) │
       └────────────────┬───────────────────┘
                        ↓
        ┌───────────────────────────────────────┐
        │   Fill Missing Ratings (User Mean)    │
        └────────────────┬──────────────────────┘
                         ↓
     ┌────────────────────────────────────────────┐
     │  Compute Cosine Similarity (User-User)     │
     └────────────────┬───────────────────────────┘
                      ↓
   ┌────────────────────────────────────────────────────────────┐
   │  Predict Ratings using Top-K Most Similar Users            │
   └────────────────┬───────────────────────────────────────────┘
                    ↓
        ┌──────────────────────────────────────────────┐
        │ Evaluate with MAE + Compare with Random Model│
        └────────────────┬─────────────────────────────┘
                         ↓
             ┌────────────────────────────┐
             │  Recommend Top-N Jokes     │
             └────────────────────────────┘

---

## 🧪 Evaluation Strategy

- **Train-Test Split**: 80% train / 20% test  
- **Similarity Measure**: Cosine Similarity  
- **Top-K** similar users evaluated for `K = [5, 10, 20, 50]`  
- **Metric**: Mean Absolute Error (MAE)  
- **Baseline**: Random K-user recommender for rating prediction  

---

## 🖥️ Code Structure (Colab Notebook)

- `data = pd.read_csv(...)`: Load ratings  
- `active_data = filter_users(...)`: Keep top users  
- `train_data, test_data = train_test_split(...)`  
- `cosine_similarity(...)`: Calculate similarity matrix  
- `predict_ratings(...)`: Predict rating using weighted K nearest neighbors  
- `evaluate_model(...)`: Evaluate model MAE  
- `random_recommender(...)`: Baseline with random K users  
- `recommend_jokes(...)`: Recommend Top-N jokes  
- `get_top_similar_users(...)`: Extract 2K top user pairs by similarity  

---

## 📈 Results Summary

| K   | Collaborative MAE | Random MAE |
|-----|-------------------|------------|
| 5   | 0.XX              | 0.XX       |
| 10  | 0.XX              | 0.XX       |
| 20  | 0.XX              | 0.XX       |
| 50  | 0.XX              | 0.XX       |

> Replace `0.XX` with actual MAE values after running your final notebook.

---

## 📌 Example Output

### 🔢 Sample Test Predictions:

---

## 🔐 Notes

- No external recommender libraries used — strictly based on course concepts.  
- Replace `API keys`, if any, with secure environment variables in production.  

---

## 🧑‍⚕️ Use Cases

- Humor personalization  
- Collaborative filtering demonstration  
- Recommender system coursework/project  

---

## 📜 License

Educational use only. For research and learning purposes. Do not use with real user-sensitive data.

---

## 🤝 Contributions

Suggestions and improvements are welcome. This system is modular — feel free to extend it with KNN, PCA, or clustering!
