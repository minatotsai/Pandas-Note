# Pandas-Note
```diff
1050. Actors and Directors Who Cooperated At Least Three Times
+ Refer to sriganesh777
- 2023/09/07
- Runtime 489ms (26.34%)/ Memory 61MB(80.87%)
  def actors_and_directors(actor_director: pd.DataFrame) -> pd.DataFrame:
    Group the data by actor_id and director_id, and count the number of cooperations
    grouped = actor_director.groupby(['actor_id', 'director_id']).size().reset_index(name='cooperation_count')

    # now 
    | actor_id | director_id | cooperation_count |
    | -------- | ----------- | ----------------- |
    | 1        | 1           | 3                 |
    | 1        | 2           | 2                 |
    | 2        | 1           | 2                 |
      
    # Filter the pairs where the cooperation count is at least three
    filtered_pairs = grouped[grouped['cooperation_count'] >= 3]
    
    return filtered_pairs[['actor_id', 'director_id']]
    | actor_id | director_id |
    | -------- | ----------- |
    | 1        | 1           |

    also can use 
    grouped = actor_director.groupby(['actor_id', 'director_id']).size().reset_index(name='cooperation_count')
    return grouped[grouped['cooperation_count']>=3][['actor_id', 'director_id']]
    
    groupby = mysql => group by
    count() = mysql => count()
    reset_index = Reset the index of the DataFrame, and use the default one instead
```
```diff
1517. Find Users With Valid E-Mails
+ Refer to Kyrylo-Ktl, Joey01
- 2023/09/09
- Runtime 691ms (5.13%) / Memory 61.40MB(16.32%)
- Runtime 464ms (25.53%)/ Memory 61.30MB(34.20%)
  def valid_emails(users: pd.DataFrame) -> pd.DataFrame:  

-   #Kyrylo-Ktl
    result = users[users['mail'].str.match(r'^[a-zA-Z][a-zA-Z\d_.-]\*@leetcode\.com')]  
  
-   #Joey01
    result = users[users['mail'].str.match(r'^[A-Za-z][A-Za-z0-9_\.\-]\*@leetcode\.com$')]
    return result
```

```diff
177. Nth Highest Salary
+ Refer to bcs636764, sriganesh777

- 2023/09/11
- Runtime 465ms (24.39%) / Memory 60.87MB(39.52%)

  def nth_highest_salary(employee: pd.DataFrame, N: int) -> pd.DataFrame:
    # Drop any duplicate salary values to avoid counting duplicates as separate salary ranks
    salaries = employee['salary'].drop_duplicates()
    # Sort the unique salaries in descending order and get the Nth highest salary
    sorted_salaries = salaries.sort_values(ascending=False)
    # If N exceeds the number of unique salaries, return None
    if N > len(sorted_salaries):
        return pd.DataFrame({f'getNthHighestSalary({N})': [None]})
    # Get the Nth highest salary from the sorted salaries
    nth_highest = sorted_salaries.iloc[ N-1 ]
    return pd.DataFrame({f'getNthHighestSalary({N})': [nth_highest]})
```

```diff
178. Rank Scores
+ Refer to prathams29

- 2023/09/12
- Runtime 646ms (5.03%) / Memory 61.83MB(54.65%)

  def nth_highest_salary(employee: pd.DataFrame, N: int) -> pd.DataFrame:
    df = scores.sort_values(by = 'score', ascending=False)
    # rank(method='dense',ascending=False) = mysql-method => DENSE_RANK() OVER (PARTITION BY column1, column2, ... ORDER BY column3 [ASC|DESC])
    df['rank'] = df['score'].rank(method='dense',ascending=False)
    return df[['score','rank']]
```

```diff
586. Customer Placing the Largest Number of Orders
+ Refer to prathams29

- 2023/09/13
- Runtime 439ms (43.5%) / Memory 60.6MB(69.94%)

  def largest_orders(orders: pd.DataFrame) -> pd.DataFrame:
    return orders['customer_number'].mode().to_frame()

  # .mode => the value that appears most frequently.
  # .to_frame() => transform it into a new DataFrame.
```
```diff
596. Classes More Than 5 Students
+ Refer to sriganesh777
- 2023/09/17
- Runtime 377ms (48.64%)/ Memory 62.13MB(13.18%)
  def find_classes(courses: pd.DataFrame) -> pd.DataFrame:
    df = courses.groupby('class')['student'].count().reset_index()
    return df[df['student'] >=5][['class']]
```





