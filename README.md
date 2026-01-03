# Overview

This project analyzes an ecommerce customer behavior dataset to uncover key factors driving customer churn, engagement, and lifetime value. Using Python for data cleaning, exploratory analysis, visualization, and predictive modeling, the study examines how customer interactions, purchasing behavior, marketing engagement, and service experience influence retention outcomes.

## Practical business questions:

1. What is the overall customer churn rate?
2. Which behavioral and engagement metrics most strongly influence churn?

3. What characteristics define high-lifetime-value customers?

4.  What are the Top 10 churn predictors?

5.  Which customer segments should be prioritized for retention strategies?


The insights from this project are intended to support data-driven decision-making for customer retention strategies, targeted marketing efforts, and revenue optimization in an ecommerce environment.

## Tools & Technologies

- Python (Pandas, Matplotlib, Seaborn, Scikit-learn)

- Jupyter Notebook

- Git & GitHub

## Data Preparation & Cleanup
This section shows the steps taken to prepare data in ensuring accuracy and consistency, cleaning to ensure data quality before intiating the task.

```python
from datasets import load_dataset
import matplotlib.pyplot as plt
import seaborn as sns
import ast
import os
path = kagglehub.dataset_download(
    "dhairyajeetsingh/ecommerce-customer-behavior-dataset"
)
file_path = os.path.join(path, 'ecommerce_customer_churn_dataset.csv')
df = pd.read_csv(file_path)
```

# 1. What is the overall customer churn rate?
The analysis evaluates the overall customer churn rate using a pie chart to compare retained and churned customers. Results show that 28.9% of customers have churned, while 71.1% remain active, providing a clear snapshot of customer retention health. This high-level metric serves as a foundation for deeper analysis into behavioral, engagement, and transactional factors that influence churn and customer lifetime value.

View my notebook with detailed steps here: [Ecommerce_Prj1.ipynb](Ecommerce_Prj1.ipynb)


## Visualize Data

```python
labels = ['Retained Customers', 'Churned Customers']
sizes = [churn_rate[0], churn_rate[1]]

plt.figure(figsize=(6, 6))
plt.pie(sizes, labels=labels, autopct='%1.1f%%', startangle=90,
    explode=(0, 0.05))  # slightly separate churned slice
plt.title('Overall Customer Churn Rate')
plt.tight_layout()
plt.show()
```

## Results

![Visualization of overall Customer Churn](Project_2\1.churn.png)
*Pie Chart visualizing the overall customers churn rate*

## Insights
- Nearly 3 out of 10 customers churn (28.9%), indicating a meaningful loss of customers over time.
- The majority of customers (71.1%) are retained, suggesting existing engagement and value strategies are working for most users.
- Reducing churn presents a clear growth opportunity, as retaining existing customers is more cost-effective than acquiring new ones.

# 2. Which behavioral factors most strongly influence churn?
From the comparison between retained and churned customers, clear gaps appear in engagement, purchasing recency, and shopping behavior. Churned customers consistently show weaker engagement signals and higher friction during the purchase journey.

View my notebook with detailed steps here: [Ecommerce_Prj1.ipynb](Ecommerce_Prj1.ipynb)

## Visualize Data
```python
behavior_summary.T.plot(
    kind='bar',
    figsize=(10, 6)
)

plt.title('Behavioral Factors Influencing Customer Churn')
plt.ylabel('Average Value')
plt.xlabel('')
plt.xticks(rotation=45)
plt.legend(title='Customer Status')
plt.tight_layout()
plt.grid(False) 
plt.show()
```
## Results
![Behavioral Factors for inflence churn](Project_2\2.Behavoiur.png)
*Bar chart visualizing behavioral differences between churned and retained customers*

## Insights
- Higher cart abandonment rate is the strongest churn signal
Churned customers abandon carts significantly more often, indicating purchase friction, pricing issues, or poor checkout experience.

- Lower engagement drives churn
Churned users log in less frequently, spend less time per session, and view fewer pages—showing weaker platform interaction overall.

- Longer time since last purchase increases churn risk
Customers who haven’t purchased recently are far more likely to churn, highlighting the importance of re-engagement strategies.

# 3.What characteristics define high-lifetime-value customers?
The boxplots compare customer behavior metrics across lifetime value (LTV) segments to identify patterns that distinguish high-value customers. Metrics include total purchases, average order value, login frequency, and cart abandonment rate. Clear distributional differences highlight behaviors associated with long-term customer value.

View my notebook with detailed steps here: [Ecommerce_Prj1.ipynb](Ecommerce_Prj1.ipynb)

## Visualize Data
```python
for i, metric in enumerate(metrics):
    sns.boxplot(
        data=df_clean,
        x='LTV_Segment',
        y=metric,
        ax=ax[i//2, i%2],
        palette='Set3')
    ax[i//2, i%2].set_title(metric)
    ax[i//2, i%2].grid(False)

plt.suptitle('Distribution of Key Behaviors by Lifetime Value Segment')
plt.tight_layout()
plt.show()
```

## Results
![High-lifetime-value customers Characteristics](Project_2\3.Highlife-Value.png)*Boxplots comparing purchasing and engagement behaviors between high and low/medium lifetime value customers*

## Insights
- High-LTV customers purchase more frequently and log in more often, indicating stronger engagement and repeat behavior.

- High-LTV customers show lower cart abandonment rates, suggesting higher purchase intent and smoother checkout experiences.

- Average order value alone does not strongly differentiate LTV, implying that retention and frequency matter more than single large purchases.

# 4. What are the Top 10 churn predictors
This visualization ranks customer behavior metrics by their correlation with churn. All shown factors have a negative correlation, meaning higher engagement or activity in these areas is associated with a lower likelihood of churn. The chart helps identify which behaviors are most important for retention-focused strategies.

View my notebook with detailed steps here: [Ecommerce_Prj1.ipynb](Ecommerce_Prj1.ipynb)

## Visualize Data
```python
plt.figure(figsize=(8, 6))
sns.barplot(
    x=top_predictors.values,
    y=top_predictors.index,
    palette='coolwarm'
)

plt.title('Top Behavioral Predictors of Customer Churn')
plt.xlabel('Correlation with Churn')
plt.ylabel('')
plt.tight_layout()
plt.show()
```
## Results
![High-lifetime-value customers Characteristics](Project_2\4.churn.png)*Top 10 horizontal bar chart titled showing the ned sgative correlation between various customer engagement metrics and churn, indicating that higher engagement is associated with lower churn rates.*

## Insights
- Session engagement metrics (pages per session anession duration) are the strongest indicators of retention, highlighting the importance of in-platform user experience.

- Digital engagement behaviors (mobile app usage and email open rate) show strong relationships with reduced churn, emphasizing the value of consistent customer touchpoints.

- Purchase-related activity (total purchases and credit balance) still matters, but behavioral engagement signals are more powerful churn predictors than spending alone.

# 5. Which customer segments should be prioritized for retention strategies?
This heatmap illustrates how churn varies across combinations of customer engagement (low, medium, high) and lifetime value (LTV). Darker cells indicate higher churn rates, allowing quick identification of high-risk customer segments and where retention efforts should be focused

View my notebook with detailed steps here: [Ecommerce_Prj1.ipynb](Ecommerce_Prj1.ipynb)

## Visualize Data
```python
plt.figure(figsize=(9, 6))

plt.title('Customer Churn by Engagement and Lifetime Value')
plt.xlabel('Lifetime Va
sns.heatmap(
    heatmap_data,
    annot=True,
    fmt=".1%",
    cmap="Reds",
    linewidths=0.5,
    cbar_kws={'label': 'Churn Rate'}lue Segment')
plt.ylabel('Engagement Level')

sns.despine(left=True, bottom=True)
plt.tight_layout()
plt.show()
```

## Results
![Customer Segments for Retention Strategies](Project_2\5.segment.png)*Heatmap visualizing customer churn rates across engagement levels and lifetime value segments.*

## Insights
- Low-engagement customers consistently exhibit the highest churn, regardless of lifetime value, making engagement the most critical retention driver.

- High-engagement customers have substantially lower churn, even among high-LTV users, highlighting the protective effect of sustained interaction.

- High-LTV but low-engagement customers represent the highest-risk, highest-impact segment, suggesting a priority target for proactive retention strategies.

# Challenges Faced

- Data quality and preparation:
The dataset required careful inspection to ensure columns were correctly interpreted (e.g., churn labels, engagement metrics, and lifetime value). Handling feature scaling and avoiding modeling errors was a key challenge.

- Feature selection and interpretation:
Identifying which behavioral metrics truly influenced churn required multiple aggregation steps, correlation checks, and visual comparisons between churned and retained customers.

- Visualization clarity:
Creating clean, professional visualizations (e.g., removing background grids, choosing appropriate chart types, and ensuring readability) required iterative adjustments to effectively communicate insights.

# Conclusions
- Customer churn is strongly linked to engagement behavior, with lower login frequency, shorter sessions, and higher cart abandonment rates consistently associated with churned customers.

- High-lifetime-value (LTV) customers demonstrate higher purchase frequency, stronger engagement, and lower churn risk, making them critical targets for retention strategies.

- Segmenting customers by engagement and lifetime value provides actionable insights that can guide marketing, personalization, and customer retention efforts.