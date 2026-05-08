# SmartCart – E-Commerce Recommender System

A big data analytics project implementing a recommendation engine and purchase pattern 
analysis for e-commerce using Collaborative Filtering and Association Rule Mining.

## Overview

SmartCart analyzes user-product interaction data to generate personalized product 
recommendations and uncover frequent purchasing patterns. The project covers the full 
pipeline from data exploration to business recommendations.

## Dataset

Two datasets are used:
- `ecommerce_user_data.csv` – User interactions with products (ratings, timestamps)
- `product_details.csv` – Product metadata (names, categories)

Both datasets are merged on `ProductID` for combined behavioral and content analysis.

## Project Structure

### Part 1 – User-Based Collaborative Filtering

**Data Preprocessing**
- Removed duplicates and merged datasets on ProductID
- Built a user-item matrix using pivot tables
- Applied one-hot encoding for transaction representation

**User Similarity Analysis**
- Computed cosine similarity between users based on rating patterns
- Analyzed category-level interactions and average ratings per user
- Split data into training (562 interactions) and testing (162 interactions) sets

**Recommendation Engine**
- Implemented a function to find top-N similar users per target user
- Generated product recommendations by aggregating scores from similar users
- Mapped ProductIDs to product names for interpretability

**Evaluation**
- Average Precision@5: 0.032
- Average Recall@5: 0.05
- Low scores attributed to data sparsity and cold-start limitations

### Part 2 – Association Rule Mining (Apriori)

**Data Preparation**
- Grouped products by user to form transaction lists
- Applied TransactionEncoder for one-hot transformation

**Apriori Algorithm**
- Mined frequent itemsets with a low min_support threshold to handle sparse data
- Generated association rules using support, confidence, and lift metrics

**Key Findings**
- Strongest pairing: Toys Item 15 + Toys Item 39
- Perfect confidence rule: Clothing Item 42 + Beauty Item 70
- Central hub product across categories: Beauty Item 70
- Cross-category bridge: Home Item 79

**Visualizations**
- Top 20 frequent items bar chart
- Association rules network diagram (edge width = lift, color = confidence)
- User similarity heatmap

## Results Summary

| Method | Metric | Score |
|---|---|---|
| Collaborative Filtering | Precision@5 | 0.032 |
| Collaborative Filtering | Recall@5 | 0.05 |
| Association Rule Mining | Top Lift Rule | Toys Item 15 + Toys Item 39 |

## Key Challenges

- **Data sparsity** – Most of the user-item matrix was empty, weakening similarity scores
- **Cold-start problem** – New users received poor recommendations due to lack of history
- **Popularity bias** – Both methods over-recommended already popular items
- **Apriori sensitivity** – Performance heavily dependent on min_support and confidence thresholds

## Business Recommendations

1. **Hybrid system** – Combine collaborative filtering with association rule mining for better coverage
2. **Content-based filtering** – Use product metadata to address cold-start issues
3. **Diversity boosting** – Re-rank recommendations to surface niche and newer products
4. **Scalable algorithms** – Replace cosine similarity with Approximate Nearest Neighbors 
   and Apriori with FP-Growth for production scalability
5. **Contextual signals** – Incorporate session behavior and temporal trends for real-time relevance

## Tech Stack

- Python, Pandas, NumPy
- Scikit-learn (cosine similarity, train/test splitting)
- MLxtend (Apriori, TransactionEncoder, association_rules)
- Matplotlib, Seaborn, NetworkX

## Team

- Gabriel Asencios
- Shashwat Shah
- Said El-Sherbiny
- Arvind Lakshmanan

Submitted for SOEN 471 – Big Data Analytics, Concordia University, April 2026.
