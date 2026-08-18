![](https://github.com/aidandig/Understanding-Customers-with-KMeans-Clustering/blob/main/images/Customer%20Cluster%20Visualization.png)

# Retail Customer Segmentation Analysis

# Project Overview

This project focuses on understanding customer behavior in order to provide executive-level actionable insights for different customer types. The executive's needs focuses on monetary value, frequency of placing orders, and recency of orders. 

## Python Packages Used

- **Data Manipulation:** pandas
- **Data Visualization:** matplotlib, seaborn
- **Machine Learning:** scikit-learn

# Data

This project utilizes UC Irvine Machine Learning Repository's [Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail) data set. It is a transactional data set containing retail data occurring between 12/1/2010 and 12/09/2011, including invoices, stocking codes, descriptions of products, item quantities, unit prices, customer IDs, and countries where the customer resides.

## Exploratory Data Analysis

Ultimately there was extra data that was unneeded for answering the executive's needs. For example, Several stock codes unrelated to customer orders (ex. accounting, postage, etc.) were included in the data set which were ultimately dropped. There were also missing customer IDs which made it impossible to correctly assign customer IDs and into the final clustering phase. There were illogical values such as negative quantities and unit prices. The EDA process focused on understanding the data's types, finding necessary information, and which information to drop.

## Data Preprocessing

1. Invoice numbers were cleaned to satisfy three types of acceptable formats: 5-digit string, 5-digit string with a letter at the end, and PADS (padding related to customer orders).
2. Missing Customer IDs were ultimately dropped because there is no reliable way of recovering the information. In a real setting, I would first work with the data engineers and other employees to attempt to recover the missing information. If not, it would still need to be dropped in order to ensure we are left with categorizing known Customer IDs into clusters.
3. Ensured that Unit Prices are above £0.00 and dropping negative values.
4. Outliers were detected by separating data 1.5 IQR above Q3 and 1.5 IQR below Q1 and saved for manual clustering analysis later on.

After the data cleaning process, 73% of the data was retained. I kept note of this percentage because the executives would likely be interested in understanding how much of their transactional data was usable for the assignment. A 27% drop is relatively fine, but I would explain to the executives my reasoning from above as to why the 27% drop was warranted.

# Results and evaluation

This project utilized KMeans Clustering to create the customer profiles. I used the elbow method alongside silhouette scoring to determine the optimal K value for the assignment. This resulted in a K value of 4, which created 4 distinct groups from the non-outlier data. The elbow method determined that 4 or 5 clusters would be optimal for the significant drop in inertia before it began to slowly plateau as K value increases. Looking at the silhouette score graph, K = 4 is a more optimal K value due to the higher silhouette score. A higher silhouette score indicates more distinct clustering and less overlap. See graphs below.

![](https://github.com/aidandig/Understanding-Customers-with-KMeans-Clustering/blob/main/images/KMeans%20Analysis.png)

Due to the different scales of Monetary Value, Frequency, and Recency, the data was scaled using scikit-learn's StandardScaler before training the KMeans model. StandardScaler retained the original shape of the data but was necessary to address larger scales further influencing the KMeans algorithm. After the KMeans model was fit with the scaled data, I plotted the original cleaned data with the cluster labels. See visualization below to see the distinct clusters.

![](https://github.com/aidandig/Understanding-Customers-with-KMeans-Clustering/blob/main/images/3D%20scatter%20plot%20of%20customer%20data.png)

After clustering, I used violin plots for Monetary Value, Frequency, and Recency to compare each of the clusters with the entire cleaned data. This ultimately led to developing the actionable insights for the 4 clusters. See visualization below.

![](https://github.com/aidandig/Understanding-Customers-with-KMeans-Clustering/blob/main/images/Cluster%20violin%20plots.png)

The same process from above was used to develop actionable insights for the outlier data. See visualization below.

![](https://github.com/aidandig/Understanding-Customers-with-KMeans-Clustering/blob/main/images/outlier%20cluster%20violin%20plots.png)

After I wrote recommendations on how to further convert each cluster into more Monetary Value, Frequency, and less recency, Customer IDs were assigned their cluster and a final [Online Retail Clustered file](https://github.com/aidandig/Understanding-Customers-with-KMeans-Clustering/blob/main/data/Online%20Retail%20Clustered.xlsx) was exported with the aggregated results.

# Final Results

Below is a final visualization report on the customer segmentation analysis. On the left y-axis it shows the number of customers per cluster bar. The line plot shows the average value for Monetary Value (per £1000, Frequency of Orders, and Recency (Days since last order as of 12/09/2011), utilizing the right y-axis. See visualization below.

![](https://github.com/aidandig/Understanding-Customers-with-KMeans-Clustering/blob/main/images/Customer%20Cluster%20Visualization.png)

The further analysis, recommendations for each cluster, and more insights are provided in the full customer segmentation analysis [Jupyter Notebook](https://github.com/aidandig/Understanding-Customers-with-KMeans-Clustering/blob/main/online-retail-clustering.ipynb).

# Citation
Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository. [https://doi.org/10.24432/C5BW33](https://doi.org/10.24432/C5BW33).

# License

The data set from this project is licensed under a [Creative Commons Attribution 4.0 International (CC BY 4.0) license](https://creativecommons.org/licenses/by/4.0/legalcode). It allows for the sharing and adaptation of the datasets for any purpose, provided that the appropriate credit is given.
