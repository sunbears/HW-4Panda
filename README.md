

```python
# HW#4 Pandas - Academy of Py
```


```python
#Dependencies
import os
import pandas as pd
```


```python
#Load 'schools_complete.cSV' file
csvpath = os.path.join('..','raw_data','schools_complete.csv')
schools = pd.read_csv(csvpath)
schools.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School ID</th>
      <th>name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Load 'students_complete.csv' file
csvpath2 = os.path.join('..','raw_data','students_complete.csv')
students = pd.read_csv(csvpath2)
students.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Student ID</th>
      <th>name</th>
      <th>gender</th>
      <th>grade</th>
      <th>school</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>Huang High School</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>Huang High School</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Merge the two files into one master data frame.

#Make school name have the same column name in both files.  Differentiate the name columns in the two files.
schools = schools.rename(columns = {'School ID': 'school_id','name': 'school_name'})
students = students.rename(columns = {'school':'school_name', 'name':'student_name','Student ID':'student_id'})
merge_df = pd.merge(schools, students, on = 'school_name')
merge_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_id</th>
      <th>school_name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>student_id</th>
      <th>student_name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>




```python
# PART 1: District Summary: High level snapshot (in table form) of the district's key metrics, including:
  #Total Schools, Total Students, Total Budget, Average Math Score, Average Reading Score
  #% Passing Math, % Passing Reading, Overall Passing Rate (Average of the above two)#Total Schoools
```


```python
#Total schools and total students
total_schools = merge_df['school_id'].nunique()
print('Total Schools: ', total_schools)

total_students = merge_df['student_id'].nunique()
print('Total Students: ', total_students)
```

    Total Schools:  15
    Total Students:  39170
    


```python
#To confirm that student_ids aren't repeated at more than one school, 
#I compared whether the number of student_id's in merge_df with the number of rows in the original students file.
total_students == students['student_id'].count()
```




    True




```python
#Total Budget: Sum up the budget across all schools, using the original schools dataframe.
total_budget = schools['budget'].sum()
total_budget = '${:,.2f}'.format(total_budget)
print('Total Budget: ', total_budget)
```

    Total Budget:  $24,649,428.00
    


```python
#Average Math and Reading Scores

avg_math = merge_df['math_score'].mean()
print('Average Math: ',round(avg_math,2))

avg_reading = merge_df['reading_score'].mean()
print('Average Reading: ', round(avg_reading,2))
```

    Average Math:  78.99
    Average Reading:  81.88
    


```python
# % Passing: Math, Reading, and Overall Passing Rate

#First confirm that there are no null score. 
#If there were NaN values, then I'd have to divide by the sum of non-NaN scores rather than by total_students.
merge_df['math_score'].isnull().values.any()
```




    False




```python
#Since there are no null values:
#Math
total_math_passing = sum(merge_df['math_score'] >= 70)
perc_math_passing = total_math_passing/total_students *100
print('% Passing Math: ', perc_math_passing)

#Reading
total_read_passing = sum(merge_df['reading_score'] >= 70)
perc_read_passing = total_read_passing/total_students *100
print('% Passing Reading: ', perc_read_passing)
```

    % Passing Math:  74.9808526934
    % Passing Reading:  85.8054633648
    


```python
#Create an Overall Score: Average of Math and Reading
merge_df['overall_score'] = (merge_df['math_score'] + merge_df['reading_score'])/2
merge_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_id</th>
      <th>school_name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>student_id</th>
      <th>student_name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>overall_score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
      <td>72.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
      <td>77.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
      <td>75.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
      <td>62.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
      <td>90.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
total_overall_passing = sum(merge_df['overall_score'] > 70)
perc_overall_passing = total_overall_passing/total_students *100
print('% Passing Overall: ', perc_overall_passing)
```

    % Passing Overall:  88.2333418432
    


```python
#District Summary Table: Putting it all together
district_summary = {'Total Schools': total_schools,
                   'Total Students': total_students,
                   'Total Budget': total_budget,
                   'Average Math Score': avg_math,
                   'Average Reading Score': avg_reading,
                   '% Passing Math': perc_math_passing,
                   '% Passing Reading': perc_read_passing,
                   '% Overall Passing Rate': perc_overall_passing}
district_summary
```




    {'% Overall Passing Rate': 88.233341843247388,
     '% Passing Math': 74.980852693387803,
     '% Passing Reading': 85.805463364820014,
     'Average Math Score': 78.98537145774827,
     'Average Reading Score': 81.87784018381414,
     'Total Budget': '$24,649,428.00',
     'Total Schools': 15,
     'Total Students': 39170}




```python
# Part 2: School Summary: Overview table that summarizes key metrics about each school, including:
# School Name, School Type, Total Students, Total School Budget, Per School Budget, Average Math Score, Average Reading Score
# % Passing Math, % Passing Reading, Overall Passing Rate (Average of the above two)
```


```python
def passing(score):
    if score >= 70:
        return 1
    else:
        return 0

merge_df['reading_pass'] = merge_df['reading_score'].apply(passing)
merge_df['math_pass'] = merge_df['math_score'].apply(passing)
merge_df['overall_pass'] = merge_df['overall_score'].apply(passing)
merge_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_id</th>
      <th>school_name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>student_id</th>
      <th>student_name</th>
      <th>gender</th>
      <th>grade</th>
      <th>reading_score</th>
      <th>math_score</th>
      <th>overall_score</th>
      <th>reading_pass</th>
      <th>math_pass</th>
      <th>overall_pass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>0</td>
      <td>Paul Bradley</td>
      <td>M</td>
      <td>9th</td>
      <td>66</td>
      <td>79</td>
      <td>72.5</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>1</td>
      <td>Victor Smith</td>
      <td>M</td>
      <td>12th</td>
      <td>94</td>
      <td>61</td>
      <td>77.5</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2</td>
      <td>Kevin Rodriguez</td>
      <td>M</td>
      <td>12th</td>
      <td>90</td>
      <td>60</td>
      <td>75.0</td>
      <td>1</td>
      <td>0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>3</td>
      <td>Dr. Richard Scott</td>
      <td>M</td>
      <td>12th</td>
      <td>67</td>
      <td>58</td>
      <td>62.5</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>4</td>
      <td>Bonnie Ray</td>
      <td>F</td>
      <td>9th</td>
      <td>97</td>
      <td>84</td>
      <td>90.5</td>
      <td>1</td>
      <td>1</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Create master grouped dataframe
school_group = merge_df.groupby('school_name')
```


```python
#Calculate count of total_students on school_group
grouped_total_students = pd.DataFrame(school_group['student_id'].count())
grouped_total_students = grouped_total_students.reset_index()
grouped_total_students = grouped_total_students.rename(columns = {'student_id': 'Total Students'})
grouped_total_students.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_name</th>
      <th>Total Students</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>4976</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>1858</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>2949</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>2739</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>1468</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Calculate sum of reading_pass, math_pass on school_group
grouped_total_pass = pd.DataFrame(school_group['reading_pass','math_pass','overall_pass'].sum())
grouped_total_pass = grouped_total_pass.reset_index()
grouped_total_pass.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_name</th>
      <th>reading_pass</th>
      <th>math_pass</th>
      <th>overall_pass</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>4077</td>
      <td>3318</td>
      <td>4239</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>1803</td>
      <td>1749</td>
      <td>1850</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>2381</td>
      <td>1946</td>
      <td>2497</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>2172</td>
      <td>1871</td>
      <td>2322</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>1426</td>
      <td>1371</td>
      <td>1460</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Calculate avg math and reading scores on school_group
grouped_avg_math_read = school_group['math_score','reading_score'].mean()
grouped_avg_math_read = grouped_avg_math_read.reset_index()
grouped_avg_math_read = grouped_avg_math_read.rename(columns = {'math_score':'Average Math Score',
                                                               'reading_score': 'Average Reading Score'})
grouped_avg_math_read.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_name</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>77.048432</td>
      <td>81.033963</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cabrera High School</td>
      <td>83.061895</td>
      <td>83.975780</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Figueroa High School</td>
      <td>76.711767</td>
      <td>81.158020</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Ford High School</td>
      <td>77.102592</td>
      <td>80.746258</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>83.351499</td>
      <td>83.816757</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Construct Data Frame of the grouped 

#When I tried to merge multiple data sets in one step, it didn't work:
#school_summary = pd.merge(schools,grouped_total_students,grouped_total_pass,grouped_avg_math_read,on = 'school_name')
#So I merged two tables at a time:

merge1 = pd.merge(schools,grouped_total_students, on = 'school_name')
merge2 = pd.merge(merge1, grouped_total_pass, on='school_name')
merge3 = pd.merge(merge2, grouped_avg_math_read, on = 'school_name')
merge3.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_id</th>
      <th>school_name</th>
      <th>type</th>
      <th>size</th>
      <th>budget</th>
      <th>Total Students</th>
      <th>reading_pass</th>
      <th>math_pass</th>
      <th>overall_pass</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>1910635</td>
      <td>2917</td>
      <td>2372</td>
      <td>1916</td>
      <td>2479</td>
      <td>76.629414</td>
      <td>81.182722</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>1884411</td>
      <td>2949</td>
      <td>2381</td>
      <td>1946</td>
      <td>2497</td>
      <td>76.711767</td>
      <td>81.158020</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>1056600</td>
      <td>1761</td>
      <td>1688</td>
      <td>1653</td>
      <td>1750</td>
      <td>83.359455</td>
      <td>83.725724</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>3022020</td>
      <td>4635</td>
      <td>3748</td>
      <td>3094</td>
      <td>3934</td>
      <td>77.289752</td>
      <td>80.934412</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>917500</td>
      <td>1468</td>
      <td>1426</td>
      <td>1371</td>
      <td>1460</td>
      <td>83.351499</td>
      <td>83.816757</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Calulate Per Student Budget
merge3['Per Student Budget'] = merge3['budget']/merge3['Total Students']
merge3['Per Student Budget'] = merge3['Per Student Budget'].map('${:,.2f}'.format)
```


```python
#Calculate Passing Percentages
merge3['% Passing Math'] = merge3['math_pass']/merge3['Total Students']*100
merge3['% Passing Reading'] = merge3['reading_pass']/merge3['Total Students']*100
merge3['% Overall Passing Rate'] = merge3['overall_pass']/merge3['Total Students']*100
```


```python
#Drop columns...size is redundant
merge4 = merge3.drop(['school_id','size', 'reading_pass', 'math_pass','overall_pass'], axis = 1)

#Rename columns
merge4 = merge4.rename(columns = {'school_name': "School Name",
                                 'type': 'School Type',
                                 'budget': 'Total School Budget'})
#Rearrange column order
merge4 = merge4[['School Name','School Type','Total Students','Total School Budget','Per Student Budget',
                'Average Math Score','Average Reading Score','% Passing Math','% Passing Reading','% Overall Passing Rate']]

#Format Total School Budget
merge4['Total School Budget'] = merge4['Total School Budget'].map("${:,.2f}".format)

merge4
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Name</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Huang High School</td>
      <td>District</td>
      <td>2917</td>
      <td>$1,910,635.00</td>
      <td>$655.00</td>
      <td>76.629414</td>
      <td>81.182722</td>
      <td>65.683922</td>
      <td>81.316421</td>
      <td>84.984573</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>$639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>84.672770</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600.00</td>
      <td>$600.00</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>99.375355</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020.00</td>
      <td>$652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>84.875944</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>$625.00</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>99.455041</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574.00</td>
      <td>$578.00</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>99.255366</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>$582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>99.569429</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Bailey High School</td>
      <td>District</td>
      <td>4976</td>
      <td>$3,124,928.00</td>
      <td>$628.00</td>
      <td>77.048432</td>
      <td>81.033963</td>
      <td>66.680064</td>
      <td>81.933280</td>
      <td>85.188907</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Holden High School</td>
      <td>Charter</td>
      <td>427</td>
      <td>$248,087.00</td>
      <td>$581.00</td>
      <td>83.803279</td>
      <td>83.814988</td>
      <td>92.505855</td>
      <td>96.252927</td>
      <td>98.594848</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Pena High School</td>
      <td>Charter</td>
      <td>962</td>
      <td>$585,858.00</td>
      <td>$609.00</td>
      <td>83.839917</td>
      <td>84.044699</td>
      <td>94.594595</td>
      <td>95.945946</td>
      <td>99.168399</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400.00</td>
      <td>$583.00</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>99.222222</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>$637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>84.746187</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650.00</td>
      <td>$650.00</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>84.982147</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>$644.00</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>84.775465</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Thomas High School</td>
      <td>Charter</td>
      <td>1635</td>
      <td>$1,043,130.00</td>
      <td>$638.00</td>
      <td>83.418349</td>
      <td>83.848930</td>
      <td>93.272171</td>
      <td>97.308869</td>
      <td>99.082569</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Part 3
#Top Performing Schools (By Passing Rate): Table of top 5 performing schools based on Overall Passing Rate. 

# Sort by % Overall Passing Rate column to find the best
merge4 = merge4.sort_values(by='% Overall Passing Rate', ascending=False)
```


```python
#Top 5 Performing Schools
top_five = merge4.iloc[:5]
top_five
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Name</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>Charter</td>
      <td>1858</td>
      <td>$1,081,356.00</td>
      <td>$582.00</td>
      <td>83.061895</td>
      <td>83.975780</td>
      <td>94.133477</td>
      <td>97.039828</td>
      <td>99.569429</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Griffin High School</td>
      <td>Charter</td>
      <td>1468</td>
      <td>$917,500.00</td>
      <td>$625.00</td>
      <td>83.351499</td>
      <td>83.816757</td>
      <td>93.392371</td>
      <td>97.138965</td>
      <td>99.455041</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Shelton High School</td>
      <td>Charter</td>
      <td>1761</td>
      <td>$1,056,600.00</td>
      <td>$600.00</td>
      <td>83.359455</td>
      <td>83.725724</td>
      <td>93.867121</td>
      <td>95.854628</td>
      <td>99.375355</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Wilson High School</td>
      <td>Charter</td>
      <td>2283</td>
      <td>$1,319,574.00</td>
      <td>$578.00</td>
      <td>83.274201</td>
      <td>83.989488</td>
      <td>93.867718</td>
      <td>96.539641</td>
      <td>99.255366</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Wright High School</td>
      <td>Charter</td>
      <td>1800</td>
      <td>$1,049,400.00</td>
      <td>$583.00</td>
      <td>83.682222</td>
      <td>83.955000</td>
      <td>93.333333</td>
      <td>96.611111</td>
      <td>99.222222</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Bottom 5 Peforming Schools

bottom_five = merge4.iloc[-5:]
bottom_five
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>School Name</th>
      <th>School Type</th>
      <th>Total Students</th>
      <th>Total School Budget</th>
      <th>Per Student Budget</th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>12</th>
      <td>Johnson High School</td>
      <td>District</td>
      <td>4761</td>
      <td>$3,094,650.00</td>
      <td>$650.00</td>
      <td>77.072464</td>
      <td>80.966394</td>
      <td>66.057551</td>
      <td>81.222432</td>
      <td>84.982147</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Hernandez High School</td>
      <td>District</td>
      <td>4635</td>
      <td>$3,022,020.00</td>
      <td>$652.00</td>
      <td>77.289752</td>
      <td>80.934412</td>
      <td>66.752967</td>
      <td>80.862999</td>
      <td>84.875944</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Ford High School</td>
      <td>District</td>
      <td>2739</td>
      <td>$1,763,916.00</td>
      <td>$644.00</td>
      <td>77.102592</td>
      <td>80.746258</td>
      <td>68.309602</td>
      <td>79.299014</td>
      <td>84.775465</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Rodriguez High School</td>
      <td>District</td>
      <td>3999</td>
      <td>$2,547,363.00</td>
      <td>$637.00</td>
      <td>76.842711</td>
      <td>80.744686</td>
      <td>66.366592</td>
      <td>80.220055</td>
      <td>84.746187</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Figueroa High School</td>
      <td>District</td>
      <td>2949</td>
      <td>$1,884,411.00</td>
      <td>$639.00</td>
      <td>76.711767</td>
      <td>81.158020</td>
      <td>65.988471</td>
      <td>80.739234</td>
      <td>84.672770</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Part 4: Math Scores by Grade: Table that lists the average Math Score for students of each grade level at each school.

grade_group = merge_df.groupby(['school_name','grade'])
grade_math = grade_group['math_score'].mean()
grade_math = pd.DataFrame(grade_math)
grade_math = grade_math.reset_index()
grade_math = grade_math.rename(columns={'math_score':'Average Math Score'})
grade_math.head(10)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_name</th>
      <th>grade</th>
      <th>Average Math Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>10th</td>
      <td>76.996772</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bailey High School</td>
      <td>11th</td>
      <td>77.515588</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bailey High School</td>
      <td>12th</td>
      <td>76.492218</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bailey High School</td>
      <td>9th</td>
      <td>77.083676</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cabrera High School</td>
      <td>10th</td>
      <td>83.154506</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Cabrera High School</td>
      <td>11th</td>
      <td>82.765560</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>12th</td>
      <td>83.277487</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Cabrera High School</td>
      <td>9th</td>
      <td>83.094697</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Figueroa High School</td>
      <td>10th</td>
      <td>76.539974</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Figueroa High School</td>
      <td>11th</td>
      <td>76.884344</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Part 5: Reading Scores by Grade
# Create a table that lists the average Reading Score for students of each grade level (9th, 10th, 11th, 12th) at each school.

grade_group = merge_df.groupby(['school_name','grade'])
grade_reading = grade_group['reading_score'].mean()
grade_reading = pd.DataFrame(grade_reading)
grade_reading = grade_reading.reset_index()
grade_reading = grade_reading.rename(columns={'reading_score':'Average Reading Score'})
grade_reading.head(10)
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>school_name</th>
      <th>grade</th>
      <th>Average Reading Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bailey High School</td>
      <td>10th</td>
      <td>80.907183</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bailey High School</td>
      <td>11th</td>
      <td>80.945643</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Bailey High School</td>
      <td>12th</td>
      <td>80.912451</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bailey High School</td>
      <td>9th</td>
      <td>81.303155</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Cabrera High School</td>
      <td>10th</td>
      <td>84.253219</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Cabrera High School</td>
      <td>11th</td>
      <td>83.788382</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cabrera High School</td>
      <td>12th</td>
      <td>84.287958</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Cabrera High School</td>
      <td>9th</td>
      <td>83.676136</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Figueroa High School</td>
      <td>10th</td>
      <td>81.408912</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Figueroa High School</td>
      <td>11th</td>
      <td>80.640339</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Part 6: Scores by School Spending
#Create a table that breaks down school performances based on average Spending Ranges (Per Student). 
#Use 4 reasonable bins to group school spending. Include in the table each of the following:
#Average Math Score, Average Reading Score, % Passing Math, % Passing Reading, Overall Passing Rate (Average of the above two)

#Convert the Per Student Budget column back to float
merge4['Per Student Budget'] = merge4['Per Student Budget'].replace('[\$,]','',regex=True).astype(float)
print(type(merge4['Per Student Budget'][0]))
```

    <class 'numpy.float64'>
    


```python
#Create the bins and group by
bins = [0,585,615,645,675]
group_names = ['<$585', '$585-615','$615-645','$645-675']
merge4['School Spend Perf'] = pd.cut(merge4['Per Student Budget'], bins, labels=group_names)
merge4_group = merge4.groupby('School Spend Perf').mean()

#Drop unnecessary columns
columns_to_drop = ['Total Students','Per Student Budget']
merge4_group.drop(columns_to_drop, axis=1, inplace = True)
merge4_group.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Spend Perf</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;$585</th>
      <td>83.455399</td>
      <td>83.933814</td>
      <td>93.460096</td>
      <td>96.610877</td>
      <td>99.160466</td>
    </tr>
    <tr>
      <th>$585-615</th>
      <td>83.599686</td>
      <td>83.885211</td>
      <td>94.230858</td>
      <td>95.900287</td>
      <td>99.271877</td>
    </tr>
    <tr>
      <th>$615-645</th>
      <td>79.079225</td>
      <td>81.891436</td>
      <td>75.668212</td>
      <td>86.106569</td>
      <td>89.653490</td>
    </tr>
    <tr>
      <th>$645-675</th>
      <td>76.997210</td>
      <td>81.027843</td>
      <td>66.164813</td>
      <td>81.133951</td>
      <td>84.947555</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Part 7: Scores by School Size
#Repeat the above breakdown, 
#but this time group schools based on a reasonable approximation of school size (Small, Medium, Large).

#Dviide the range evenly into thirds to get 3 bins
range = (merge4['Total Students'].max()) - (merge4['Total Students'].min())
bin_size = int(range/3)
bin_1_max = merge4['Total Students'].min() + bin_size
bin_2_max = bin_1_max + bin_size

bins = [merge4['Total Students'].min(), bin_1_max, bin_2_max, merge4['Total Students'].max()]
print(bins)

```

    [427, 1943, 3459, 4976]
    


```python
group_names = ['Small','Medium', 'Large']

merge4['School Size'] = pd.cut(merge4['Total Students'], bins, labels = group_names)
merge4_size_group = merge4.groupby('School Size').mean()
merge4_size_group.drop(columns_to_drop, axis=1, inplace = True)
merge4_size_group.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Size</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Small</th>
      <td>83.452223</td>
      <td>83.894482</td>
      <td>93.765511</td>
      <td>96.649891</td>
      <td>99.312169</td>
    </tr>
    <tr>
      <th>Medium</th>
      <td>78.429493</td>
      <td>81.769122</td>
      <td>73.462428</td>
      <td>84.473577</td>
      <td>88.422044</td>
    </tr>
    <tr>
      <th>Large</th>
      <td>77.063340</td>
      <td>80.919864</td>
      <td>66.464293</td>
      <td>81.059691</td>
      <td>84.948296</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Part 8: Scores by School Type
#Repeat the above breakdown, 
#but this time group schools based on school type (Charter vs. District)

merge4_type_group = merge4.groupby('School Type').mean()
merge4_type_group.drop(columns_to_drop, axis = 1, inplace = True)
merge4_type_group.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average Math Score</th>
      <th>Average Reading Score</th>
      <th>% Passing Math</th>
      <th>% Passing Reading</th>
      <th>% Overall Passing Rate</th>
    </tr>
    <tr>
      <th>School Type</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Charter</th>
      <td>83.473852</td>
      <td>83.896421</td>
      <td>93.620830</td>
      <td>96.586489</td>
      <td>99.215404</td>
    </tr>
    <tr>
      <th>District</th>
      <td>76.956733</td>
      <td>80.966636</td>
      <td>66.548453</td>
      <td>80.799062</td>
      <td>84.889428</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Three Observable Trends

#1. Suprisingly, school budgets over $615 per student had a ten percentage point lower overall passing rate.
#than school budgets less than $615 per student.

#2.  As I would have guessed, there seems to be a tsrend of overall passing rates increasing with smaller school size.

#3. Charter schools have better student performance than district schools.

#4. One thing to consider are confounding factors such as family income level of student.
#If this was controlled for, I wonder if we would see a statistically significant impact of
#school budget, size, and school typ on student performance.

```
