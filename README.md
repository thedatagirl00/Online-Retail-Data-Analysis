# Online-Retail-Data-Analysis
This project involves an exploratory data analysis (EDA) of an online retail transactional dataset. The goal is to understand the dataset's structure, clean the data by handling missing values and duplicates, and derive initial insights into customer behavior, popular products, and sales patterns across different countries.
# Data Source
The dataset used is Online Retail.xlsx, which contains transactional data from a UK-based online retailer.

# Libraries Used
pandas for data manipulation and analysis
numpy for numerical operations
matplotlib.pyplot for basic plotting
seaborn for advanced visualizations
sklearn.cluster (specifically KMeans) for potential future clustering tasks
scipy.stats for statistical functions (e.g., linregress)
plotly.graph_objects for interactive visualizations
# Data Loading and Initial Inspection
Loaded the dataset: The Online Retail.xlsx file was loaded into a pandas DataFrame named Onlretail.
Initial Data Overview: Displayed the first 25 rows using Onlretail.head(25) to get a quick glimpse of the data structure and content.
# Data Information: Used Onlretail.info() to check data types, non-null counts, and memory usage. Key observations:
Description and CustomerID columns had missing values.
InvoiceDate was correctly identified as datetime64[ns].
InvoiceNo, StockCode, Description, and Country were identified as object (categorical) types.
Shape of the Data: Confirmed the number of rows and columns using Onlretail.shape (initial: 541909 rows, 8 columns).
Summary Statistics: Onlretail.describe() provided statistical summaries for numerical columns, revealing potential issues like negative Quantity and UnitPrice values.
# Data Cleaning
# Handling Missing Values:
Identified missing values using Onlretail.isnull().sum().
Description: 1454 missing values.
CustomerID: 135080 missing values (a significant portion).
Decision: Rows with missing values in both Description and CustomerID were dropped using dropna(subset=['Description'], inplace=True) and dropna(subset=['CustomerID'], inplace=True). This was done to avoid biased conclusions, especially given the large number of missing CustomerID entries, which are crucial for customer-centric analysis.
Verification: Onlretail.isnull().sum() confirmed no remaining missing values.
# Handling Duplicates:
Checked for duplicate rows using Onlretail.duplicated().
Removed duplicate rows using Onlretail.drop_duplicates(inplace=True).
Verification: Onlretail.duplicated().sum() confirmed zero duplicate rows remaining.
Result: The dataset size was reduced from 541909 rows to 401604 rows after cleaning.
Initial Exploratory Data Analysis (EDA)
Unique Values: Explored the number of unique values in each column using Onlretail.nunique(). Noted that InvoiceNo had 22190 unique values and CustomerID had 4372, indicating many transactions per customer and invoice.
Categorical Data: Displayed categorical columns using Onlretail.select_dtypes(include='object'). It was highlighted that InvoiceNo, despite containing numbers, functions as a categorical identifier for transactions rather than a numerical variable for calculations.
Cancelled Transactions: Identified and analyzed transactions where InvoiceNo starts with 'C', indicating cancelled orders.
Filtered these transactions into a DataFrame C.
C.shape showed 8872 cancelled transactions.
Calculated that approximately 2.21% of the transactions were cancelled.
Product Analysis:
Found the StockCode with the highest frequency: 85123A.
Identified the product description for 85123A as 'WHITE HANGING HEART T-LIGHT HOLDER'.
Insight: This product is the most frequently purchased. A recommendation was made to invest more in its marketing and consider bundled promotions.
# Top 10 Stock Codes by Frequency:
Calculated the percentage frequency of the top 10 most frequent StockCode values.
Visualized these frequencies using a horizontal bar plot, showing the distribution of popular products.
Country Analysis:
Identified 37 unique countries in the dataset.
Used Onlretail['Country'].value_counts() to find the frequency of transactions by country. The United Kingdom significantly dominates the sales volume.
Explored transactions from 'Unspecified' country, noting that it had 241 records with 213 unique product descriptions.
Next Steps (Potential Future Analysis)
Further investigate negative quantities and unit prices (likely returns or adjustments).
Calculate sales revenue for each transaction (Quantity * UnitPrice).
Perform RFM (Recency, Frequency, Monetary) analysis for customer segmentation.
Analyze time-series trends in sales.
Build a recommendation system based on product co-occurrence.
Geographic analysis of sales data.
