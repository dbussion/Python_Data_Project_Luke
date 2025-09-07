# Overview

This project explores the demand, salary, and optimal skills for the top data roles in Spain in 2023. By combining job posting data with salary information, the analysis identifies which skills are essential, trending, well-compensated, and most strategic for data analysts in the Spanish labor market.


# Background

The Spanish data job market is dynamic, shaped by both traditional business intelligence tools and modern programming, cloud, and machine learning skills. To assess this landscape, the project examined:

The most demanded skills for the top 3 data roles.

Yearly trends in analyst skill requirements.

Salary distributions across key data jobs.

The alignment (or mismatch) between skill demand and pay.

The most “optimal” skills combining demand with salary outcomes.


# Tools Used

Python (pandas, seaborn, matplotlib) for data wrangling and visualization.

Jupyter Notebooks for exploration and documentation.

Dataset: “lukebarousse/data_jobs” from Hugging Face.


# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles in Spain?

To find the most demanded skills for the top 3 most popular data roles in Spain. I filtered out those positions by which ones were the most popular, and got the top 5 skills for those top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting.


### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')
for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skills_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
```

### Results

![Visualization of top skill in most demanded data roles in Spain](images/Top_skills_in_most_demanded_data_roles_.png)


### Insights

Across data roles, SQL is the universal foundation, Python is indispensable, BI tools define analysts, and cloud/big data skills distinguish engineers, while data scientists rely most on Python with some support from SQL and R.



## 2. How are in-demand skills trending for Data Analysts in Spain

### Visualize Data

```python

from matplotlib.ticker import PercentFormatter

df_plot = df_DA_SPA_percent.iloc[:, :5]

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()

plt.show()

```

![Trending Top Skills for Data Analysts in Spain in 2023](images/Trending_top_skills_DA_SPA_2023_.png)


### Insights

In 2023, SQL clearly dominated job postings for data analysts in Spain, consistently appearing in around 60–75% of advertisements and establishing itself as the core technical requirement. Python followed as the second most in-demand skill, maintaining steady relevance at 40–50% with a notable mid-year peak in July. Power BI showed more volatile demand, fluctuating widely between 20% and 50%, with sharp surges in March, June, and November, suggesting episodic but significant interest. Tableau, in contrast, displayed a relatively stable presence at 25–35%, with a modest upward trend towards the end of the year. Excel, once foundational, exhibited a gradual decline, dropping from nearly 30% in January to below that threshold mid-year and closing the year with reduced prominence. Collectively, these patterns suggest that SQL and Python remain indispensable, Power BI reflects shifting but important business intelligence needs, while Tableau holds steady as a secondary visualization tool and Excel continues to recede in importance.



## 3. How well do jobs and skills pay for Data Analysts in Spain in 2023?

### Salary Analysis

#### Visualize Data

```python
sns.boxplot(data=df_SPA_top6, x='salary_year_avg', y='job_title_short', order=job_order)
sns.set_theme(style='ticks')

plt.title('SALARY DISTRIBUTIONS IN SPAIN')
plt.xlabel('Yearly Salary (USD)')
plt.ylabel('')
plt.xlim(0, 600000)
ticks_x =plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show() 

```

#### Results

![Salary Distributions of Data Jobs in Spain in 2023](images/Salary_Distributions_Spain_.png)
*Box plot visualizing the salary distributions for the top 6 data job titles.*

#### Insights

The salary distribution plot for data-related roles in Spain highlights distinct patterns across job categories. Senior Data Engineers and Data Engineers occupy the higher salary ranges, with most earnings clustered around USD 100K–150K, indicating that engineering-focused roles are among the best compensated. Machine Learning Engineers also demonstrate broad salary variability, with a distribution stretching beyond USD 200K, reflecting both strong demand and specialized skill premiums. Data Scientists show a narrower spread, generally below USD 120K, though a few outliers suggest occasional high-paying opportunities. In contrast, Data Analysts and Senior Data Analysts earn comparatively lower salaries, mostly concentrated between USD 60K–100K, with fewer upper outliers, underscoring their relatively modest pay scale within the data profession. Overall, the hierarchy suggests that engineering and machine learning expertise command the highest rewards, while analytical roles, despite their prevalence, remain less lucrative in the Spanish market.

### Highest paid and most demanded skills for Data Analysts in Spain in 2023

#### Visualize Data

```python

fig, ax = plt.subplots(2, 1)

sns.barplot(data=df_DA_top_pay, x='median', y=df_DA_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r')
ax[0].legend().remove()

sns.barplot(data=df_DA_top_skills, x='median', y=df_DA_top_skills.index, ax=ax[1], hue='median', palette='light:b')
ax[1].legend().remove()

plt.show() 
```


#### Results

![The highest paid and most in-demand skills for Data Analysts in Spain in 2023](images/Top_paid_and_top_in-demand_skills_DA_SPA_2023_.png)


#### Insights

The comparison between highest-paid and most in-demand skills for data analysts in Spain reveals a striking divergence between market value and popularity. On the salary side, specialized tools and programming environments such as **Smartsheet, SAP, and npm** command the highest median pay, with Smartsheet standing out significantly above the rest at nearly USD 160K, highlighting the premium for niche enterprise and workflow management expertise. Other high-paying skills, including **Node.js, React, Angular, and scikit-learn**, emphasize the value of software engineering and machine learning integration within analytics roles. Conversely, the most in-demand skills reflect the everyday toolkit of data analysts: **Looker, Pandas, Jupyter, and Python** dominate job postings, underscoring the centrality of data manipulation, visualization, and scripting in practice. Widely adopted platforms such as **SQL, Excel, Power BI, and Tableau** remain highly requested but are associated with comparatively lower pay, suggesting their ubiquity reduces wage differentiation. Collectively, this contrast shows that employers most frequently seek mainstream, accessible tools, yet the highest compensation is reserved for rarer, more technical, or enterprise-focused skillsets.



## 4. What is the most optimal skill to learn for Data Analysts in Spain in 2023?

### Visualize Data

```python

from adjustText import adjust_text
from matplotlib.ticker import PercentFormatter

df_DA_skills_high_demand.plot(kind='scatter', x='skill_percent', y='median_salary')

texts = []

for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand['skill_percent'].iloc[i], df_DA_skills_high_demand['median_salary'].iloc[i], txt))

adjust_text(texts, arrowprops=dict(arrowstyle="->", color='r', lw=0.5))

ax = plt.gca()

ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))

plt.show()

```

### Results

![Most optimal skills for Data Analysts in Spain in 2023](images/Most_optimal_skills_DA_SPA_2023_.png)
*Scatter plot visualizing the most optimal skills (pay X demand) for data analytst in Spain in 2023.*


### Insights

This chart shows the most optimal skills for data analysts in Spain, balancing both salary outcomes and market demand.

SQL and Python stand out as the most demanded skills, required by nearly half of data analyst roles. SQL, in particular, dominates with >50% demand, though the salary premium is moderate (~$95K). These remain essential baseline competencies.

Analyst tools such as Tableau offer a strong balance, with ~30% demand and ~$98K salaries, making them highly attractive for employability and decent pay.

High-paying but niche skills include Looker, Pandas, and Jupyter, which command ~$105–110K but appear in only ~10–15% of postings. These are valuable differentiators for analysts aiming at specialized or more technical roles.

Cloud and infrastructure skills like Snowflake (~$90K, ~10% demand) provide an additional layer of competitiveness, though they are not yet mainstream.

In contrast, traditional tools such as Excel, Power BI, and Word show relatively low salaries (~$72–77K) and limited demand (<20%), indicating they are less optimal as differentiators, though still relevant in some entry-level or support contexts.

CONCLUSION: To maximize both employability and compensation in Spain, analysts should build strong foundations in SQL and Python, complement them with Tableau for versatility, and then strategically add high-paying but niche skills like Looker or Pandas to gain an edge.


# Main Learning

SQL is the universal baseline skill across roles.

Python is indispensable for analysts and scientists.

BI tools (Tableau, Power BI) remain central but show diverging trends.

Cloud/big data tools (Snowflake, Airflow) are emerging differentiators.

Salary premiums favor specialized or niche technical skills (e.g., Looker, Smartsheet, npm) rather than mainstream tools.

# Insights

Demand vs. Pay Mismatch: Employers seek mainstream tools like SQL, Python, and Excel most often, yet these pay less due to ubiquity.

High-Pay, Low-Demand Skills: Skills like Smartsheet, Looker, or React command salaries >$100K but appear in <15% of postings, marking them as niche differentiators.

Trends: SQL and Python remain stable anchors; Power BI shows volatility with episodic demand spikes; Excel continues to decline.

Role Salaries: Engineers (data and ML) consistently earn more than analysts, with senior engineers at the top of the range.

# Final Conclusion

For data analysts in Spain, the optimal career strategy is to master SQL and Python as core foundations, strengthen versatility with Tableau, and strategically add niche, high-paying skills such as Looker, Pandas, or Snowflake. This layered skillset maximizes both employability and salary potential.

*Credit: This project was guided step-by-step by Luke Barousse’s Python for Data Analytics – Full Course for Beginners, which provided both the dataset and foundational methods for data analysis.*
