# Purchase Order Categorization Solution

## Overview
A scalable solution for categorizing multilingual purchase order items using NLP and semantic clustering, developed for BuildNow's take-home assessment.

## Setup Instructions
**1. Run in Google Colab:**  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/esraasiyamek/buildnow_AI_Task/blob/main/categorize_items.ipynb)

**2. Requirements:**
- Google account
- OpenAI API key (free tier sufficient for testing)
- 'purchase-order-items.xlsx' dataset

**3. Setup Steps:**
1. Open the notebook in Colab using the badge above
2. Add your OpenAI API key when prompted
3. upload the dataset file
4. Run all cells sequentially (Runtime → Run all)
   *Note: Translation and embedding steps may take 20-40 minutes for 3000 items*

## Technical Approach

### Chosen Methodlogy: Clustering with Text Embeddings
**Why Clustering with Text Embeddings?**
Clustering with text embeddings was chosen as it enables automatic categorization of multilingual purchase order items without requiring predefined rules or extensive domain knowledge. Given the diverse nature of construction-related items and their descriptions, a rule-based approach struggled due to the variety of terminologies, abbreviations, and multilingual content.

Text embeddings, generated using OpenAI's text-embedding-3-large model, convert item descriptions into numerical vectors that capture their semantic meaning. Clustering these vectors using K-means allows similar items to be grouped together based on their context rather than relying on exact keyword matches.

### Methodology
1. **Data Cleaning**  
   - Removed measurements/special characters using regex
   - Standardized multilingual text
   - Removed null and overly short descriptions.

2. **Item Categorization**  
   - **Translation**: Arabic descriptions were translated into English using GPT-3.5.Initial attempts at clustering without translation resulted in separate Arabic and English clusters, leading to suboptimal grouping.
   - **Embeddings**: Transformed item descriptions into high-dimensional vector representations using OpenAI’s text-embedding model.
   - **Clustering**: Applied K-means clustering with a fixed number of 10 categories.
   - **Automated Labeling**: Used GPT-3.5-turbo to generate meaningful labels for clusters, reducing manual effort.While this step helps automate labeling, it can be replaced with domain expertise for better accuracy.

3. **Analysis**  
  - Item distribution across categories.
  - Number of items per category.
  - Spending by category.
  - Identification of top-spending items.

### Comparison with Alternative Approaches

**Rule-Based Approach (Hybrid Attempt)**
Initially, a rule-based approach was considered using a predefined dictionary of construction-related keywords mapped to categories. However, due to limited domain knowledge in construction terminology, defining comprehensive keyword lists proved challenging. The hybrid approach combined:

Step 1: Rule-based categorization using keyword matching.

Step 2: ML-based categorization for uncategorized items using clustering.

This approach resulted in only 800 out of 3000 data entries being categorized in the first step, leaving 2200 items unclassified. Given the inconsistency and limitations of keyword-based categorization, clustering with text embeddings was chosen as the primary method.


### Improvements & Scalability
| Aspect          | Current Implementation | Production-Ready Approach       |
|-----------------|------------------------|----------------------------------|
| Translation     | GPT-3.5 per-item       | Batch API calls with caching    |
| Embeddings      | OpenAI API             | Fine-tuned local model          |
| Clustering      | K-means                | HDBSCAN with dynamic categories |

### Future Roadmap
- Real-time categorization API
- Supplier-specific trend analysis
- Automated taxonomy updates

---

## Results & Insights

### Key Findings
- **Category Distribution**:
  - Most Common: Building Fixtures & Hardware (559 items)
  - Most Valuable: Reinforcing Steel Products (90,012 BCY/item)
- **Spending Patterns**:
  - Top 3 Categories: 51.4% of total spending
  - Highest Spending: Building Fixtures & Hardware (27,295,818.98 BCY)

### Recommendations
1. **Credit Strategy**:
   - Prioritize Steel Bars category (high spend/volume ratio)
   - Develop category-specific risk models
2. **Data Quality**:
   - Standardize descriptions in Building Fixtures
   - Add measurement unit metadata
3. **Supplier Relations**:
   - Negotiate bulk pricing for high-variance items
   - Develop alternative supplier pipeline

### Challenges Overcome
- **Multilingual Handling**: Unified Arabic/English items through translation
- **Messy Descriptions**: Regex cleaning + semantic clustering
- **Cluster Validation**: LLM-assisted labeling

### Future Improvements
- Add sub-category taxonomy
- Implement real-time processing
- Integrate supplier performance metrics

