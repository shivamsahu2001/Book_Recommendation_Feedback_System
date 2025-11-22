# 📚 Book Recommendation Feedback System

A production-ready **Machine Learning-based Book Recommendation System** built using **Collaborative Filtering**, powered by Python and deployed using **Streamlit**.  
This project demonstrates a complete recommendation workflow including data preprocessing, model creation, and interactive UI.

---

# 🚀 Project Overview

This system recommends books to users based on popularity as well as similarity scores.  
It features two major components:

### ⭐ 1. Popularity-Based Top 50 Books  
Books are displayed in a **5 × 10 grid layout**, showing:  
- Book Cover  
- Book Title  
- Author  

Loaded using `popular.pkl`.

### ⭐ 2. Similar Book Recommendations (Top 5)  
Users select a book from the dropdown → The system returns the **top 5 similar books**.  
Each recommendation includes:  
- Cover Image  
- Title  
- Author  

---

# 🖼️ Screenshots

### 📌 Popularity-Based Top 50 Books  
Add your screenshot here after uploading to GitHub:
![Top 50 Books](images/popularity_screenshot.png)

### 📌 Similar Book Recommendations  
Add your screenshot here:
![Similar Books](images/recommendation_screenshot.png)

> Create an `images/` folder in your repo and upload screenshots there.

---

# 📁 Project Structure

```
📦 Book-Recommendation-System
│
├── app.py                     → Streamlit UI
├── Recommender.ipynb          → Model creation notebook
│
├── books.pkl                  → Cleaned metadata
├── popular.pkl                → Top 50 books data
├── pt.pkl                     → Pivot table for collaborative filtering
├── similarity_scores.pkl      → Cosine similarity matrix
│
├── Data/
│   ├── Books.csv
│   ├── Ratings.csv
│   └── Users.csv
│
└── README.md
```

---

# 📊 Data Used

### 📘 **Books.csv**
Contains metadata:  
- ISBN  
- Book Title  
- Author  
- Image URLs  

### ⭐ **Ratings.csv**
Contains user ratings:  
- User ID  
- ISBN  
- Rating Value  

### 🧑‍🤝‍🧑 **Users.csv**
Contains demographic information:  
- User ID  
- Age  
- Location  

These CSV files were used to build pivot tables and similarity scores, later stored as `.pkl` files.

---

# 🧠 How the Recommendation Model Works

The system uses **Collaborative Filtering**:

- A pivot table of users × books (`pt.pkl`)  
- Cosine similarity score matrix (`similarity_scores.pkl`)  
- Metadata lookup via `books.pkl`

### 🔍 Recommendation Logic  
```
1. Take the selected book
2. Find its index in the pivot table
3. Retrieve similarity scores
4. Sort scores in descending order
5. Extract top 5 similar books
```

---

# ⭐ Core Recommendation Function

```python
def recommend(book_name):
    index = np.where(pt.index == book_name)[0][0]
    similar_items = sorted(
        list(enumerate(similarity_scores[index])),
        key=lambda x: x[1],
        reverse=True
    )[1:6]

    data = []
    for i in similar_items:
        temp_df = books[books['Book-Title'] == pt.index[i[0]]]
        item = [
            temp_df.drop_duplicates('Book-Title')['Book-Title'].values[0],
            temp_df.drop_duplicates('Book-Title')['Book-Author'].values[0],
            temp_df.drop_duplicates('Book-Title')['Image-URL-M'].values[0]
        ]
        data.append(item)
    return data
```

---

# ▶️ How to Run the Project

### **1. Clone the repository**
```bash
git clone https://github.com/your-username/Book-Recommendation-Feedback-System.git
cd Book-Recommendation-Feedback-System
```

### **2. Install dependencies**
```bash
pip install -r requirements.txt
```

### **3. Run the Streamlit app**
```bash
streamlit run app.py
```

### **4. Open in browser**
```
http://localhost:8501/
```

---

# 🔮 Future Enhancements

- Add NLP-based content filtering  
- Add user accounts & personalized recommendations  
- Deploy online via Streamlit Cloud or Render  
- Add category-based filtering  
- Add rating submission and feedback mechanism  

---

# 📄 License
MIT License  
