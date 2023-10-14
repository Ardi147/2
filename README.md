# 1. Data Basics
# 1.1 Define the concept of data
Data is a collection of facts, information, or values that are recorded, stored, or represented in various forms, such as numbers, text, images, sound, or other formats.
# 1.2 Describe basic data variable types 
## - boolean
In Python, the bool data type is used to represent boolean values (True, False). Booleans are used to evaluate expressions and return the boolean True or False based on the result of the expression.

         x = 10
         y = 5
         result = x > y
         print(result)
         print(type(result))
## - numeric
The numeric data type in Python represents the data that has a numeric value. A numeric value can be an integer, a floating number, or even a complex number. These values are defined as Python int, Python float, and Python complex classes in Python.
## - string
In Python, the str data type is used to define text component enclosing a sequence of characters within single-quotes or double-quotes. Python strings can contain letters, numbers or special characters.

         platform = "JC Chouinard"

         print(type(platform))
         print(platform)
# 1.3 Describe basic structures used in data analytics
## - tables
Tables are used to structured data, it is essentially a two-dimensional structure with rows and columns.
## - rows
Rows, also known as records or observations, are the horizontal elements in a table.
## - columns
Columns, also known as fields or variables, are the vertical elements in a table. Each column represents a specific attribute or piece of information related to the data set.
## - lists
While tables are used for structured data, lists are used for storing unstructured or semi-structured data. A list is a collection of items, where each item can be of a different data type or structure. Lists are often used for tasks like storing unstructured text data, logs, or simple collections of values.
# 1.4 Describe data categories
## - qualitative
Survey responses where participants choose from option like “Yes” or “No”.
## - quantitative
Sales data showing the number of products sold and prices.
## - structured
- Structured data is data that organized and formatted in a way that easy to read
- Student records are stored in the university’s SQL database, containing columns such as Student_ID, Student Name, and Major
## - unstructured
- Unstructured data has no particular structure and is difficult to organize or categorize
- This includes Text, images, audio, and video files
- Example : Social media posts, email, images, audio recording.
## - metadata
Metadata in this context refers to information about the healthcare data. It includes details such as data source, data format, data creation timestamp, patient ID, data quality, and more.
## - big data
The healthcare system collects patient records, medical images, sensor data from wearable devices, electronic health records (EHRs), and more.
# 2. Data Manipulation
These data manipulation techniques are crucial for data preparation and analysis in various domains, from business analytics to data science and machine learning. They help ensure data quality, consistency, and usability for decision-making and reporting.
# 2.1 Import, store, and export data 
Fundamental understanding of ETL (Extract, Transform, Load): ETL is a process used in data management to extract data from various sources, transform it into a consistent format, and load it into a destination such as a data warehouse or a database. It involves the following steps:
## Fundamental understanding of ETL:
## - extract
extract the file into .csv format

         df.to_csv("D:/MyEduSolve/tugas_cleansing.csv")
## - transform
         df['Referal'] = df['Referal'].astype(str)

         df['Referal'] = df['Referal'].replace({'1.0': 'Use', '0.0': 'Not use'})
## - load
load a CSV file containing datasets from online stores obtained from Kaggle

         df = pd.read_csv('online_store.csv')
## - common data storage file formats (delimited data files, XML, JSON)
         df = pd.read_csv('online_store.csv')
# 2.2 Clean data
Purpose and common practices:
## - handling NULL
Dealing with missing or NULL values, which may involve imputing missing data or excluding rows with missing values.
example : 
Check data condition
Input: 

         df.info()

Display a visualization of the columns Age.
Input: 

         df.Age.plot(kind='hist')

Because the Age column has a skewness distribution. Then we will do imputation on the Age column using the median.
Input: 
         
         val = df.Age.median()
         df['Age'] = df.Age.fillna(val)
         
Display dataset info to see whether the Age column has been imputed
Input: 

         df.info()
## - special characters
Removing or encoding special characters that can cause data processing issues.
example : 
You have the file name
Input: 

         df = pd.read_csv('online_store!!.csv')
         
And the double exclamation mark special character (!!) can cause problems when trying to read or process such files. You can remove these special character to make the file name cleaner and more easily accessible.

After removing special characters, the filename will become
Input: 

         df = pd.read_csv('online_store.csv')
## - trimming spaces
Trimming leading and trailing white spaces from text data to ensure consistency.
example :
Suppose you have text “ jupyter notebook “ that has extra spaces at the front and at the back. By trimming the extra spaces, the text will become:
“jupyter notebook”
This ensures that the text does not have unnecessary spaces at the beginning or end, thereby ensuring consistency in text formatting and avoiding problems that can occur when searching or processing data.
## - inconsistent formatting
Standardizing data formats, such as date formats, to make them consistent.
example : 
change the data format in the date column to YYYY-MM-DD for consistency
## - removing duplicates 
Identifying and removing duplicate records to ensure data accuracy.
example :
Input:

      df.duplicated().sum()
      df_new = df.drop_duplicates()
      df_new.duplicated().sum()
## - imputing data
Filling in missing data with appropriate values based on rules or algorithms.
example : 
Input:     
      
         df.Gender[df.Gender.isnull()]
         df.Gender.value_counts() 
         val = df.Gender.mode().values[0]
         df['Gender'] = df.Gender.fillna(val)
         df.Gender.value_counts()
## - validating data
Checking data for correctness and validity to ensure it meets predefined criteria or constraints
example : 
Before starting validation, it is important to examine the data by understanding the structure, data types, and any potential problems. It can use the head(), info(), and describe() methods of pandas DataFrame for this purpose.
Input:   
      
         df.head()
         df.info()
         
Based on the results of the data inspection, it was found that the referral column used the float data type, this was deemed unsuitable, the data would be easier to understand if converted into a string, where "1.0" means using a referral code, while "0.0" means not using a code referral. This will help people who read the data so that it is easier to understand. (Data Type Validating)
Input:  
      
         df['Referal'] = df['Referal'].astype(str)
         df['Referal'] = df['Referal'].replace({1.0: 'Use', 0.0: 'Not use'})
## 2.3 Organize data
Purpose and common practices:
## - sorting
Reordering data based on one or more columns, usually in ascending or descending order.
Example:
Input: 

         data = {'Name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve’], 'Age': [25, 30, 22, 35, 28], 'Salary': [50000, 60000, 45000, 70000, 55000]}
         sorted_data = sorted(zip(data['Name'], data['Age'], data['Salary']), key=lambda x: x[1])
         print("Sorted data by Age:", sorted_data)
# - filtering
Selecting a subset of data based on specified criteria.
Example:
Input:

         filtered_data = [(name, age, salary) for name, age, salary in zip(data['Name'], data['Age'], data['Salary']) if age > 25]
         print("Filtered data:", filtered_data)
## - slicing
Extracting a specific range or portion of the data.
Example:
Input:

         sliced_data = (data['Name'][1:3], data['Age'][1:3], data['Salary'][1:3])
         print("Sliced data:", sliced_data)
## - transposing 
Changing the orientation of data, such as converting rows to columns or vice versa.
Example:
Input: 

         transposed_data = {'Name': data['Name'], 'Age': data['Age'], 'Salary': data['Salary']}
         print("Transposed data:", list(zip(*transposed_data.values())))
## - appending
Combining or adding new data to an existing dataset.
Example:
Input:

         new_data = {'Name': ['Frank', 'Grace'], 'Age': [29, 32], 'Salary': [52000, 60000]}
         appended_data = {key: data[key] + new_data[key] for key in data}
         print("Appended data:", appended_data)
## - truncating
Reducing the data to a specific length or number of rows, often to create smaller subsets of data.
Example:
Input:

         truncated_data = {key: data[key][:3] for key in data}
         print("Truncated data:", truncated_data)
# 2.4 Aggregate data
## Purpose and common practices:
## - grouping
- Grouping SUM is an aggregation function that calculates the sum of a specific numerical column within each group. When you group data by one or more columns, you can apply the SUM function to find the total sum of a particular numerical value for each group.
- Grouping COUNT is an aggregation function that counts the number of rows within each group. It is used to determine how many items fall into each group.
- Grouping AVG is an aggregation function that calculates the average (mean) of a specific numerical column within each group. This function provides the average value of the data in each group. 
## - joining/merging 
Combining data from multiple sources or tables using keys or common columns.
## - summarizing
Creating summary statistics or aggregations to get an overview of the data, such as calculating totals, averages, or counts.
## - pivoting
Restructuring data to transform rows into columns or vice versa, often used for creating summary tables or pivot tables.
