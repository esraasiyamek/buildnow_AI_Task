# buildnow_AI_Task

# Purchase Order Categorization Solution

## Overview
A scalable solution for categorizing multilingual purchase order items using NLP and clustering with text embedding, developed for BuildNow's take-home assessment.

## Setup Instructions
**1. Run in Google Colab:**  
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/esraasiyamek/buildnow_AI_Task/blob/main/categorize_items.ipynb)

**2. Requirements:**
- Google account
- OpenAI API key (free tier sufficient for testing)
- prupurchase-order-items.xlsx dataset

**3. Setup Steps:**
1. Open the notebook in Colab using the badge above
2. Add your OpenAI API key when prompted
3. upload the dataset file
4. Run all cells sequentially (Runtime → Run all)
   *Note: Translation and embedding steps may take 20-40 minutes for 3000 items*

## Technical Approach#

**Choses Methodlogy: Clustering with Text Embeddings**
Why Clustering with Text Embeddings?

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

**Comparison with Alternative Approaches**

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


**Key Findings**  

**Category Distribution**:
- The most common categories are Building Fixtures & Hardware with 559 items.
- The least common categories are Copper Wiring Supplies, Reinforcement Steel Products, Lighting Fixtures with only 148 items each.

**Spending Pattern**s:
- The highest spending is in Building Fixtures & Hardware category with 27295818.98 BCY.
- The category with highest average spending per item is Reinforcing Steel Products at 90012.23687747035 BCY per item.


  **Recommendations**  
- Focus credit offerings on Building Fixtures & Hardware, Reinforcing Steel Products, Steel Bars which account for 51.4% of total spending.
- Investigate the Steel Bars category which has few items but significant spending.
- Consider standardizing descriptions for Building Fixtures & Hardware to improve categorization.

  **Future Improvement**  
- Expand the taxonomy with sub-categories for more granular analysis.
- Implement real-time categorization for new purchase orders.
- Add supplier information to analyze category-supplier relationships. 


