# 🖥️ Web Server Log Analysis Using Apache Spark

## 📊 Project Overview
This project involves analyzing web server log data using Apache Spark to extract meaningful insights from a large dataset. By processing over 1 million log entries, this project identifies important traffic patterns, tracks errors, and monitors server performance.

## 📁 Dataset
The dataset used is an Apache Web Server log file in the Common Log Format (CLF). It consists of over 1 million log entries from the NASA Kennedy Space Center server. Each log entry provides detailed information about web requests, including timestamps, IP addresses, HTTP methods, response codes, and content sizes.

## 🚀 Key Features
- **Log Parsing**: Corrected initial errors in parsing using refined regular expressions, successfully processing over 99.99% of log entries.
- **Error Analysis**: Analyzed 404 (Not Found) error patterns by day, hour, and specific URLs.
- **Traffic Monitoring**: Generated insights into traffic distribution across days, hours, and by specific endpoints.
- **Visualization**: Used Matplotlib to visualize trends, including hourly 404 errors, response codes, and traffic patterns.

## 📋 Steps to Run the Project
1. **Set Up Environment**: Ensure Java 8 is installed for PySpark to function properly. Run the following command in your environment:
    ```bash
    !apt install openjdk-8-jdk-headless -qq
    ```
2. **Install PySpark**: Install the required PySpark package.
    ```bash
    !pip install pyspark
    ```
3. **Download the Dataset**: Download the NASA web server log dataset from [this link](http://ita.ee.lbl.gov/html/contrib/NASA-HTTP.html).
4. **Run the Analysis**: Load the dataset and run the provided Spark scripts to perform log parsing, error tracking, and traffic analysis.

## 📈 Results
- **Log Parsing Success Rate**: 99.99% of logs were successfully parsed after regular expression refinement.
- **Top 404 Errors**: Identified the top 20 URLs responsible for 404 errors, revealing common broken links.
- **Traffic Insights**: Analyzed traffic patterns and identified peak activity hours and days.

 Developed a web server log analysis system using PySpark to process and analyze Apache server logs.
-	Corrected 108 parsing errors in the initial dataset by refining regular expressions, achieving a 99.99% log parsing success rate.
-	Conducted analysis of over 1 million log entries, producing insights such as top endpoints, response codes, and traffic patterns by day and hour.
-	Visualized key metrics like the top error-prone endpoints and 404 response code trends using Matplotlib, enhancing the ability to monitor server performance and detect issues.


## 📊 Visualization
Key metrics are visualized using Matplotlib, showcasing trends like:
- **Top 404 Error URLs**: This bar chart displays the top 20 URLs that caused the most 404 errors.

```python
# Top 20 404 Error URLs Data
urls, counts = zip(*badEndpointsTop20)

# Bar Chart Visualization
fig = plt.figure(figsize=(10,6), facecolor='white', edgecolor='white')
plt.barh(urls, counts, color='skyblue')
plt.xlabel('Number of 404 Errors')
plt.ylabel('URL')
plt.title('Top 20 URLs Causing 404 Errors')
plt.tight_layout()
plt.show()
```
![image](https://github.com/user-attachments/assets/489cd677-2f33-4826-afcd-2cd78a9bbf59)

- **Hourly 404 Error Distribution**: This line graph displays the distribution of 404 errors across different hours of the day.

```python
# Hourly 404 Errors Data
hoursWithErrors404 = hourRecordsSorted.map(lambda a: a[0]).collect()
errors404ByHours = hourRecordsSorted.map(lambda a: a[1]).collect()

# Line Graph Visualization
fig = plt.figure(figsize=(8,4.2), facecolor='white', edgecolor='white')
plt.axis([0, max(hoursWithErrors404), 0, max(errors404ByHours)])
plt.grid(visible=True, which='major', axis='y')
plt.xlabel('Hour of Day')
plt.ylabel('Number of 404 Errors')
plt.plot(hoursWithErrors404, errors404ByHours)
plt.title('Hourly Distribution of 404 Errors')
plt.show()
```
![image](https://github.com/user-attachments/assets/dab25119-2d05-46ef-a352-0c95492201d8)

- **Daily Traffic Patterns**: This line graph visualizes the number of 404 errors recorded for each day.
```python
# Daily 404 Errors Data
daysWithErrors404 = errDateSorted.map(lambda ab: ab[0]).collect()
errors404ByDay = errDateSorted.map(lambda ab: ab[1]).collect()

# Line Graph Visualization
fig = plt.figure(figsize=(8,4.2), facecolor='white', edgecolor='white')
plt.axis([0, max(daysWithErrors404), 0, max(errors404ByDay)])
plt.grid(visible=True, which='major', axis='y')
plt.xlabel('Day of Month')
plt.ylabel('Number of 404 Errors')
plt.plot(daysWithErrors404, errors404ByDay)
plt.title('Daily Distribution of 404 Errors')
plt.show()
```
![image](https://github.com/user-attachments/assets/c1e4c144-35e6-4df2-9c27-2176e424d62f)

## 🔮 Future Work
- Extend the analysis to other server logs and integrate real-time monitoring.
- Implement machine learning models for predictive log analysis to identify potential issues in advance.
- Incorporate a user interface to provide real-time visual feedback.

