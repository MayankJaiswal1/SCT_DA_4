# 📊 Marketing Campaign Performance — EDA & Budget Recommendation

> Exploratory Data Analysis on 200,000 marketing campaigns to answer one business question: **should budget be reallocated between marketing channels based on ROI?**

No predictive model here on purpose — the brief was to focus on the **"why,"** not the "what's next."

![Python](https://img.shields.io/badge/Python-3.10-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Cleaning-150458?logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C)
![SciPy](https://img.shields.io/badge/SciPy-ANOVA%20Testing-8CAAE6?logo=scipy&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## 🧭 TL;DR

After cleaning the data, mapping the funnel, and statistically testing ROI across every channel, campaign type, audience, and location cut in the dataset:

> 🚫 **No channel is a statistically significant ROI winner** (one-way ANOVA, all p > 0.17).

The headline recommendation is to **not** make a large ROI-driven budget shift, and to stop treating ROI as the sole decision metric. Full reasoning is in the 📄 [1-page report](Marketing_ROI_Report.docx).

---

## 🗂️ Dataset

📦 [Marketing Campaign Performance Dataset](https://www.kaggle.com/datasets/manishabhatt22/marketing-campaign-performance-dataset) — Kaggle

200,000 campaigns spanning 2021, across:
- 📢 6 channels — Facebook, Website, Google Ads, Email, YouTube, Instagram
- 🎯 5 campaign types
- 🌍 Multiple audiences, locations, and customer segments

---

## 📁 Repo Contents

| File | What it is |
|---|---|
| 📓 `eda_marketing_campaign.ipynb` | Full analysis notebook — cleaning, funnel, ROI/significance testing, all charts, pre-run with outputs |
| 📄 `Marketing_ROI_Report.docx` | 1-page business report with the executive summary and budget recommendation |
| 🗃️ `marketing_campaign_dataset.csv` | Raw source data *(gitignored — download from Kaggle, see Setup)* |
| 🧹 `marketing_campaign_clean.csv` | Cleaned dataset with engineered fields (`Conversions`, `CTR`, `Cost_per_Conversion`) *(gitignored — regenerate by running the notebook)* |
| 📈 `channel_summary.csv` | Channel-level rollup (spend, ROI, conversion rate, cost-efficiency) |
| 🔻 `funnel_overall.png` | Impressions → Clicks → Conversions funnel |
| 🔻 `funnel_by_channel.png` | CTR and click-to-conversion rate, split by channel |
| 💰 `roi_by_channel.png` | Average ROI by channel with 95% confidence intervals |
| 💸 `cost_per_conversion.png` | Cost-efficiency ranking by channel |
| 🫧 `spend_vs_roi.png` | Spend vs. ROI bubble chart (bubble size = total conversions) |

---

## ⚙️ Setup

The raw and cleaned CSVs aren't committed (200K rows / ~30–60MB each — not great to store in git). To reproduce:

```bash
pip install pandas numpy scipy matplotlib jupyter

# Download the raw CSV from Kaggle and place it in the repo root as:
# marketing_campaign_dataset.csv
# https://www.kaggle.com/datasets/manishabhatt22/marketing-campaign-performance-dataset

jupyter nbconvert --to notebook --execute --inplace eda_marketing_campaign.ipynb
```

This regenerates `marketing_campaign_clean.csv`, `channel_summary.csv`, and all five chart PNGs. ✅

---

## 🔬 Approach

**1️⃣ Clean**
- Parsed `Duration` (`"30 days"` → `30`) and `Acquisition_Cost` (`"$1,234.56"` → `1234.56`)
- Verified 0 nulls, 0 duplicates, and no logic errors (e.g. clicks never exceed impressions)
- Engineered `Conversions` (= Clicks × Conversion_Rate), `CTR`, and `Cost_per_Conversion`

**2️⃣ Visualize the funnel**
- Impressions → Clicks → Conversions, overall and by channel
- ~14% of impressions become clicks, ~1.1% become conversions — consistent across every channel

**3️⃣ Test, don't just rank**
- A plain bar chart will always show a "top" channel. Before recommending anything, every metric (ROI, conversion rate, CTR, cost-per-conversion, engagement) was run through a **one-way ANOVA** across channels.
- Result: none of it is statistically significant. Differences in the raw numbers are within normal random variation for this data.

**4️⃣ Recommend based on evidence, not noise**

| Channel | Avg ROI | Cost / Conversion | Spend Share |
|---|---|---|---|
| 🥇 Facebook | 5.019x | $637.91 | 16.4% |
| 🥈 Website | 5.014x | $636.86 | 16.7% |
| Google Ads | 5.003x | $647.64 | 16.8% |
| Email | 4.996x | $637.07 | 16.8% |
| YouTube | 4.994x | $640.90 | 16.7% |
| Instagram | 4.989x | $639.995 | 16.7% |

Current spend is already split almost evenly. Given the lack of significance, the report recommends **holding that allocation**, with at most a small (~5–10%) tilt toward Website/Facebook, and shifting focus to incrementality testing (holdout/geo experiments) rather than ROI ranking as the budget-decision metric.

---

## 🛠️ Tools

| Tool | Purpose | Link |
|---|---|---|
| 🐍 Python 3 | Core language | https://www.python.org/ |
| 🐼 pandas | Data cleaning & aggregation | https://pandas.pydata.org/ |
| 🔢 NumPy | Numerical operations | https://numpy.org/ |
| 📐 SciPy | ANOVA significance testing | https://scipy.org/ |
| 📊 Matplotlib | Charts & visualizations | https://matplotlib.org/ |
| 📓 Jupyter | Notebook environment | https://jupyter.org/ |
| 📝 docx (npm) | Word report generation | https://www.npmjs.com/package/docx |

---

## 👤 Author

**Mayank Jaiswal**
Data Analyst 
