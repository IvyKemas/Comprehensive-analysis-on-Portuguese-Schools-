# Comprehensive-analysis-on-Portuguese-Schools

## Project Overview: Methodical Exploration and Insight Generation in Portuguese School Data

This initiative rigorously applies advanced methodologies, including comprehensive Exploratory Data Analysis (EDA), foundational data comprehension, and the strategic generation of visually compelling representations. The primary objective is to derive actionable insights by conducting an in-depth analysis of the Portuguese Schools dataset (student-mat). This systematic approach not only enhances our understanding of the dataset but also contributes valuable perspectives for informed decision-making in the educational domain.

## Table of Contents:

1. [Understanding the Data](#Initial-Data-Understanding)
2. [Exploratory Data Analyis](#Exploratory-Data-Analyis)
3. [Correlation Analysis](#Correlation-Analysis)
4. [Group Comparison](#Group-Comparison))
5. [Conclusion](#Conclusion)
6. [Recommendations](#Recommendations)

# Initial-Data-Understanding
In this phase, the dataset was loaded, and an initial understanding was sought. The data set, named "student-mat," comprises 395 entries and encompasses 33 columns. These columns capture diverse attributes, such as demographic information, academic performance, and lifestyle choices of Portuguese students. This thorough exploration lays the foundation for subsequent analyses, allowing for a nuanced understanding of the dataset's characteristics

## Loading and Understanding the Data
```{r}
library(readr)
student_mat <- read_csv("C:/Users/ADMIN/Desktop/End-semesters STA 2040/student-mat.csv")
View(student_mat)
```
Here, the dataset was loaded using the readr library, offering a glimpse into its structure and contents.

## Exploring the Dataset
```{r}
# Getting the shape of the dataset
shape=dim(student_mat)
shape
# Get the column names of the dataset
column_names=colnames(student_mat)
print(column_names)
# Summary of numeric columns
summary(student_mat[c("age", "absences", "G1", "G2", "G3","Medu", "Fedu", "traveltime", "studytime", "failures", "famrel","freetime", "goout", "Dalc", "Walc", "health")])
```
This section provides insights into the dataset's dimensions, column names, and a summary of numeric attributes, offering a comprehensive overview.
## Dataset Structure
```{r}
# Generate the structure of the dataset
str(student_mat)
```
The structure of the dataset is revealed, illustrating the data types of each attribute.
## Data Preview
```{r}
# Previewing the first few rows of the dataset
head(student_mat)
# Previewing the last few rows of the dataset
tail(student_mat)
```
The initial rows of the dataset are displayed, providing a preview of the data.
## Insights Gained during this phase 

- **Dataset Description:** The dataset comprises 395 entries and 33 columns, providing comprehensive information about individual students across diverse parameters.
- **Shape of the Dataset:** The data includes details on various aspects of 395 students, with each student described by 33 different attributes.
- **Column Names:** The columns cover a wide range of information, encompassing school details, gender, age, address, family size, parental education, and academic performance.
- **Summary of Numeric Columns:** A thorough summary of numeric attributes is provided, offering insights into age, absences, and grades (G1, G2, G3). This summary encompasses key statistics like minimum, maximum, median, mean, and quartiles.
- **Insights from Numeric Columns:**
- Age: The age of students ranges from 15 to 22, with an average (mean) age of approximately 16.7.
- Absences: The number of absences varies from 0 to 75, with an average of about 5.709.
- Grades (G1, G2, G3): Grades show a spread from 3 to 19, with mean values around 10.91, 10.71, and 10.42, respectively.
- Other Numeric Columns: Similar patterns are observed across various attributes, with detailed statistics provided for each numeric column, including parental education, travel time, study time, failures, family relationships, free time, social outings, alcohol consumption, and health status.
  
# Exploratory-Data-Analyis
Exploratory Data Analysis (EDA) is conducted to gain insights into the dataset containing information about individual students. I proceeded to ensure the variables are categorized into three types: Categorical, Discrete Numerical, and Continuous Numerical. Visualizations are generated for each category to comprehend the distribution of student characteristics.

## Categorical Variables:
Visualizations are created for categorical variables, such as school, gender, address, family size, and more. Interpretations are provided for each variable, offering insights into the distribution of students across different categories.
```{r}
# Load the necessary libraries
library(ggplot2)

# Categorical variables
categorical_vars <- c("school", "sex", "address", "famsize", "Pstatus", "Mjob", "Fjob", "reason","guardian", "schoolsup", "famsup", "paid", "activities", "nursery", "higher", "internet", "romantic")

for (var in categorical_vars) {
  p <- ggplot(student_mat, aes_string(x = var, fill = var)) +
    geom_bar(stat = "count") +
    geom_text(stat = "count", aes(label = ..count..), vjust = -0.5, size = 3) +
    labs(title = paste("Distribution of", var),
         x = var,
         y = "Count") +
    theme_minimal()
  
  print(p)
}
```
<img width="499" alt="Screenshot 2023-12-02 224822" src="https://github.com/IvyKemas/Comprehensive-analysis-on-Portuguese-Schools-/assets/122665283/8d0410d0-2607-4914-8f48-34d9da0a5bb6">
<img width="502" alt="Screenshot 2023-12-02 224938" src="https://github.com/IvyKemas/Comprehensive-analysis-on-Portuguese-Schools-/assets/122665283/c79d40cd-2d7c-49a4-86c9-f70172a98d8c">
The above are some of the visualizations generated for the categorical variables.

## Discrete Numerical Variables:
Bar charts are generated for discrete numerical variables like mother's education, father's education, travel time, study time, and more. Each chart provides a detailed analysis of the distribution of students based on these discrete numerical attributes.
```{r}
# Load the necessary library
library(ggplot2)

# Discrete numerical variables
discrete_numeric_vars <- c("Medu", "Fedu", "traveltime", "studytime", "failures", "famrel",
                           "freetime", "goout", "Dalc", "Walc", "health")

# Loop through each discrete numerical variable
for (var in discrete_numeric_vars) {
  # Create a bar plot
  p <- ggplot(student_mat, aes_string(x = as.factor(student_mat[[var]]), fill = as.factor(student_mat[[var]]))) +
    geom_bar() +
    labs(title = paste("Distribution of", var),
         x = var,
         y = "Count") +
    theme_minimal() +
    # Add text annotations for count
    geom_text(stat='count', aes(label=..count..), vjust=-0.5, size=4)
  
  # Print the plot
  print(p)
}
```
<img width="499" alt="Screenshot 2023-12-02 225538" src="https://github.com/IvyKemas/Comprehensive-analysis-on-Portuguese-Schools-/assets/122665283/fbbcd865-5112-4ef5-86da-354165c52a99">
<img width="494" alt="Screenshot 2023-12-02 225737" src="https://github.com/IvyKemas/Comprehensive-analysis-on-Portuguese-Schools-/assets/122665283/1f9cb51c-f709-4cef-8bdc-416bc8bee79e">
Above is a glimpse of some of the visualizations generated from the Discrete Numerical Variables.

## Continuous Numerical Variables:
Density plots are created for continuous numerical variables, including age, absences, and grades (G1, G2, G3). Each plot is accompanied by an interpretation, discussing the distribution characteristics and potential outliers in the data.
```{r}
# Load the necessary library
library(ggplot2)

# Continuous numerical variables
continuous_numeric_vars <- c("age", "absences", "G1", "G2", "G3")

# Loop through each continuous numerical variable
for (var in continuous_numeric_vars) {
  # Create a density plot
  p <- ggplot(student_mat, aes_string(x = var)) +
    geom_density(fill = "purple", alpha = 0.5) +
    labs(title = paste("Distribution of", var),
         x = var,
         y = "Density") +
    theme_minimal()
  
  # Print the plot
  print(p)
}
```
<img width="506" alt="Screenshot 2023-12-02 230125" src="https://github.com/IvyKemas/Comprehensive-analysis-on-Portuguese-Schools-/assets/122665283/b2495f22-33ea-4efb-9660-b37e5f3717a6">
<img width="493" alt="Screenshot 2023-12-02 230203" src="https://github.com/IvyKemas/Comprehensive-analysis-on-Portuguese-Schools-/assets/122665283/d9b2a44c-a063-473e-9290-8d80319a6274">
Above are some of the visualiations generated.

## Correlation-Analysis
Understanding the intricate connections between various factors and student performance is crucial for unraveling key insights within the dataset. In this section, a comprehensive Correlation Analysis is conducted to quantify the relationships among key numerical variables and academic outcomes. The primary objective is to compute a correlation matrix, revealing the strength and direction of associations.

```{r}
# Load the necessary libraries
library(ggplot2)
library(reshape2)

# Select the relevant numerical variables for correlation analysis
correlation_vars <- c("age", "Medu", "Fedu", "traveltime", "studytime", "failures", "famrel",
                      "freetime", "goout", "Dalc", "Walc", "health", "absences", "G1", "G2", "G3")

# Compute the correlation matrix
correlation_matrix <- cor(student_mat[correlation_vars])

# Convert the correlation matrix to a long format for visualization
correlation_data <- melt(correlation_matrix)

# Create a heatmap visualization with customized colors
heatmap_plot <- ggplot(correlation_data, aes(Var1, Var2, fill = value)) +
  geom_tile(color = "white") +
  scale_fill_gradient2(low = "blue", mid = "pink", high = "red", midpoint = 0,
                       limits = c(-1, 1), name = "Correlation") +
  labs(title = "Correlation Heatmap",
       x = "Variables",
       y = "Variables",
       fill = "Correlation") +
  theme_minimal() +
  theme(axis.text.x = element_text(angle = 45, hjust = 1))

# Calculate the correlation values
correlation_values <- as.data.frame(as.table(correlation_matrix))
colnames(correlation_values) <- c("Variable1", "Variable2", "Correlation")

# Print the heatmap
print(heatmap_plot)
```
<img width="496" alt="Screenshot 2023-12-03 014010" src="https://github.com/IvyKemas/Comprehensive-analysis-on-Portuguese-Schools-/assets/122665283/6a18bd9d-e5db-4d5f-a1e0-c6bf0bd8dc19">

In the correlation heatmap, the variables with the strongest positive correlations are:
- G2 and G3 (Second period grade and Final grade): 0.905
This indicates a very strong positive relationship between a student’s performance in the second period and their final grade. Students who perform well in the second period are likely to achieve high final grades. G1 and G2 (First period grade and Second period grade): 0.852

- There is a strong positive relationship between a student’s performance in the first period and their performance in the second period. Good performance in the first period is associated with good performance in the second period.

# Group-Comparison
In the group comparison analysis, my focus was on understanding how different groups within the student population were performing across various factors. To ensure the robustness of the findings and account for variations in sample sizes, I employed the 'survey' library in R. This allowed me to implement weighted analyses, providing more accurate estimates that consider the differential influence of distinct groups. Utilizing the survey design framework, I performed weighted comparisons in specific categories. Below are the findings.

## Student Achievement Across Schools:
Employing box plots, I compared the final grades of students from two different schools, "GP" and "MS." The use of weighted analysis provided me with a nuanced perspective, highlighting the impact of each school on the overall performance. This approach considered both the median and variability, allowing for a more comprehensive understanding of how each school contributed to the academic landscape.

## Analyzing Grade Variances by Guardian:
In grouping students based on guardianship, I conducted a detailed analysis using box plots. Leveraging the 'survey' library enabled me to address the varying sample sizes across different guardian categories. By focusing on fathers, mothers, and other guardians, I unveiled distinct patterns and variations in student outcomes. This individualized examination provided insights into the specific influences of different guardians on student academic performance.

## Analyzing Grade Variances by Sex:
Delving into the gender-based comparison of final grades, I initially used box plots. Subsequently, I implemented weighted analyses for females and males to account for the differences in the number of students in each category. This approach provided me with a more accurate depiction of the average performance and variance within each gender group. Through these analyses, I gained a personalized understanding of how gender dynamics may influence student achievement in the academic context.
<img width="494" alt="Screenshot 2023-12-03 015517" src="https://github.com/IvyKemas/Comprehensive-analysis-on-Portuguese-Schools-/assets/122665283/58bb5424-6134-4e9d-8485-fc6d9a3ad7a0">
 
 bar plot with error bars to visualize the grade variances by sex, taking into account the difference in weights.

# Conclusion
The analysis of the dataset encompassing students from two schools, "GP" and "MS," revealed valuable insights into factors influencing academic performance. The positive correlation between study time and final grades suggests the importance of effective time management for students. Additionally, the impact of guardian categories on academic outcomes, with students having mothers as guardians showing the highest performance, adds a nuanced layer to our understanding.

Gender, family size, and parents' cohabitation status also emerge as factors affecting academic performance, albeit with varying degrees of significance and variability. The findings contribute to a deeper comprehension of the multifaceted dynamics influencing student achievement.

# Recommendations
**Promote Effective Study Habits:**
Encourage students to allocate more time for studying and consider implementing study skill workshops. By fostering effective study techniques, time management, and self-discipline, students can enhance their academic performance.

**Targeted Support for Family Size:**
Acknowledge the variability in mean grades based on family size. Provide additional support and resources for students from larger families (GT3) to help them manage their academic responsibilities alongside family commitments.

**Parental Engagement Programs:**
Recognize the significant impact of a cohabiting family environment on academic performance. Develop programs to enhance parental engagement and communication, particularly for students with non-cohabiting parents. This support could contribute to improving their academic success.

**Utilize G2 Performance for Prediction:**
Leverage the strong positive correlation between G2 (Second period grade) and final grades (G3) to identify students who might need additional support early on. Intervene for those with lower G2 scores to help them improve their overall performance.

**Targeted Assistance for "MS" School:**
Consider providing additional academic support to students in the "MS" school, especially those with lower grades. Address potential challenges they may be facing and offer resources to help them improve their performance. Tailoring assistance to the specific needs of this school can contribute to overall academic enhancement.
