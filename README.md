# 📈 What Drives Healthcare Supplement Sales on Amazon?

**A Data-Driven Exploration**  
*By Trisha Ganatra, Business Analyst | Product Analyst | ex-L'Oréal*

---

## 🚀 Business Objective

Large and small supplement brands alike struggle to understand which product listing levers truly move the needle on Amazon. This project delivers a turnkey pipeline—from live data pull to machine learning and unsupervised segmentation—to:

1. **Predict** which products will break into the ‘Top Seller’ tier (>1,000 estimated monthly units).  
2. **Reveal** hidden product clusters to inform portfolio and go-to-market strategy.  
3. **Surface** the most influential listing features (e.g. review velocity, rating, video content, pricing, offers, subscribe & save - what should brands focus on) 

---

## 🔍 Approach & Methodology

### 1. Live Data Acquisition  
- **Browser Automation** with Selenium: Scraped ASIN, price, review count & rating, ad type, Prime & Subscribe-&-Save flags for 20 high-intent keywords.  
- **Keepa API Integration**: Enriched with historical rank data, A+ Content, video presence.  

### 2. Feature Engineering & EDA  
- **Sales Buckets**: Mapped Keepa rank → Low (<100), Medium (100–1k), High (1k–10k), Top (>10k) tiers as proxies for volume.  
- **Log-Transformation** of review counts to normalize heavy right-skew.  
- **Format Analysis**: Stacked bars & heatmaps to compare price & format mix across sales tiers.  

### 3. Predictive Modeling (Supervised)  
| Model                  | AUC  | Accuracy | Key Drivers                      |
| ---------------------- | ---- | -------- | -------------------------------- |
| **Logistic Regression**| 0.85 | 79%      | Review velocity, price, video    |
| **XGBoost Classifier** | 0.82 | 78%      | Review velocity, video count     |
| **Random Forest**      | 0.82 | 78%      | Review count, ratings, price  |

> **Business takeaway:** Review growth & video content are the strongest levers for landing in the top-seller tier—regardless of format.

### 4. Product Segmentation (Unsupervised)  
- **K-Means + PCA** revealed four actionable clusters:  
  1. **Premium, Low-Rated** — high price, limited traction (new niche or overpriced).  
  2. **Popular, Trusted** — mass-market appeal; highest share of Top sellers.  
  3. **Budget, Low-Content** — low price, modest reviews/video; high upside if visibility improved.  
  4. **Unrated/Low-Quality** — poor ratings & minimal content; consider product reformulation or delisting.

> **Business takeaway:** The “Popular, Trusted” cluster is the clearest white-space for new entrants—packages that combine strong reviews, competitive pricing, and videos - not offers, subsribe and save, prime eligibility, etc

---

## 💡 Key Insights & Recommendations

- **Reviews Matter Most:** Accelerate review velocity via early-stage sampling, follow-up emails, or bundled incentives.  
- **Video & A+ Content:** Invest in 60-second demos and enhanced branding flows—Top sellers almost always feature rich media.  
- **Pricing Strategy:** Premium formats (powders, liquids) can command higher margins; mass-market formats (gummies, tablets) win on volume.  
- **Cluster-Driven Launches:** Use cluster profiles to position new SKUs—e.g. budget supplements need targeted ads; premium needs tailored brand story.  

---

## ⚠️ Limitations

1. **No True Sales Data**  
   – We infer “units sold” via Keepa rank drops (e.g. 90-day rank deltas), not actual Amazon sales figures.  
   – True revenue or volume could alter “Top Seller” labels.

2. **Snapshot-Only Dataset**  
   – Lack of rolling 30-day historical snapshots prevented time-series forecasting of review growth or seasonality.

3. **Metadata Gaps**  
   – Missing key drivers like ad spend, keyword bid data, seller inventory levels, or detailed customer demographics.

4. **Format Imbalance**  
   – Capsules >50% of SKUs; niches like liquid, powder, gummy are under-represented, which may skew cluster definitions.

5. **Proxy Features Only**  
   – Flags such as “Subscribe and Save” and “Prime Eligible” capture availability but not actual conversion uplift or repeat purchase.

---

## 📂 Repository Contents

```text
├── data/                     # raw & cleaned CSV exports
├── notebooks/                # step-by-step EDA, modeling, clustering
├── scripts/                  # reusable Python modules (scraper.py, fe.py, model.py)
├── models/                   # saved pipelines & artifacts
├── figures/                  # final charts for poster & slides
└── README.md                 # this overview
