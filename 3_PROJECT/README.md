# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles in Spain?

To find the most demanded skills for the top 3 most popular data roles in Spain. I filtered out those positions by which ones were the most popular, and got the top 5 skills for those top 3 roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting.

View my notebook with detailed steps here: [2_Skills_Demand_.ipynb](3_PROJECT\2_Skills_Demand_.ipynb)

### Visualize Data

'''python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')
for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skills_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')

plt.show()
'''

### Results

![Visualization of top skill in most demanded data roles in Spain](3_PROJECT\images\Top_skills_in_most_demanded_data_roles_.png)


