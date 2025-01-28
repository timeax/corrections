# correction_session
## TABLE OF CONTENTS 
- [DAY ONE TASK](#day-ONE-task)
- [DAY TWO TASK](#day-two-task)
- [DAY THREE PART 1](#day-three-part-1)
- [DAY THREE PART 2](#day_three-part-2)
- [ASSIGNMENT](#assignment)
---

### DAY ONE TASK:  How Many People Use Python, SQL, Excel, and Power BI in Their Current Roles?
---
**code** 
```sql 
-- Day One
SELECT t.Tools, COUNT(t.ID) AS No_of_Users
FROM tools t
   JOIN challenge c
       ON t.ID = c.ID
WHERE t.Tools IN ("python", "sql", "excel", "powerbi")
   AND c.Job_struggle 
       IN ("yes","no")   
GROUP BY Tools
ORDER BY No_of_Users
DESC;
```
---
![TASK 1](https://github.com/user-attachments/assets/bfadc078-539f-40f4-8533-01e9c9e93882)

---
**Purpose**
The purpose of the query is to determine how many users are using specific tools (Python, SQL, Excel, Power BI) in their current roles.
**Tables Involved**
- tools: This table contains information about the tools used by individuals. It has an ID field that identifies each user and a Tools field that specifies the name of the tool used.

- challenge: This table was used because we want to identify users who are working in a data role which we can pick out of the job struggle column.

#### **Query Logic**

Joining the Tables: The query uses a JOIN operation to connect the tools and challenge tables. This connection is made via the ID field, meaning it matches each tool with its corresponding User ID.

**Filtering Data:**

The query filters to only include users who are using one of the specific tools: Python, SQL, Excel, or Power BI.
It also filters out records where users haven't specified whether they face job struggles by checking that the Job_struggle field contains "yes" or "no." Understanding the dataset the job struggle column indirectly indicates if a user is already in an employment or not.
Counting Users: For each of the specified tools, the query counts how many users are using that particular tool in their current rool. It does so by counting the number of occurrences of each ID associated with each tool.

Grouping Results: The results are grouped by tool, meaning each tool (Python, SQL, Excel, Power BI) will have its own count of users.

Sorting: The final result is sorted by the number of users, in descending order. The tool with the highest number of users will appear first.

Expected Outcome
The output will display a list of tools (Python, SQL, Excel, Power BI) and the number of users associated with each tool, sorted by the most popular tool (highest user count) to the least popular.

Key Points to Note
The query combines data from two tables: one representing tools used and the other for extracting users in a data role.
It filters based on specific tools and Data job employment status.
The query counts users per tool and provides a ranking based on the number of users.


## DAY TWO TASK 
**QUESTION** : Identify the Most Popular Tools by Experience Level

---
```sql
-- Day 2 
SELECT 
     c.Experience,
     (t.tools) AS Popular_tools,
     COUNT(DISTINCT c.ID) AS tools_count       
FROM 
       challenge c
     JOIN 
       tools t 
     ON 
       c.ID = t.ID           
GROUP BY 
       c.Experience, t.Tools
ORDER BY
       c.Experience, tools_count DESC; 
```
---
![TASK 2](https://github.com/user-attachments/assets/24ea2d59-2f83-4f4e-9f4e-2872a03dd16c)

---
This SQL query aims to identify the most popular tools used by people of different experience levels. Here's a breakdown of how it works:

1. **Select Fields**: 
   - The query selects two key pieces of information: 
     - The experience level (`c.Experience`) of the individuals.
     - The specific tool(s) used by them (`t.Tools`).
   - It also retrieves how many unique individuals (`c.ID`) used each tool, using `COUNT(DISTINCT c.ID)`.

2. **From and Join**: 
   - It retrieves data from two tables: `challenge` (represented by alias `c`) and `tools` (represented by alias `t`).
   - The `JOIN` is performed based on a common field, `ID`, linking individuals in the `challenge` table to the tools they used in the `tools` table.

3. **Grouping**: 
   - The query groups the results by two things: 
     - `c.Experience`: the experience level of the individual.
     - `t.Tools`: the specific tool they used.

4. **Ordering**: 
   - The results are ordered first by the `Experience` level of the individuals, and then by the count of users per tool in descending order. This helps to see which tools are the most popular within each experience group.


## DAY THREE PART 1
**QUESTION**  : DAY 3: Retrieve Rows Where Respondents Report "Communication Skills" as a Valuable Skill and Have Fewer Than 2 Years of Experience

---
```sql
-- TASK 3
SELECT * 
FROM  challenge
WHERE Valuable_skill LIKE "%communication%" 
   AND Experience = "less than a year";        
```
---
![TASK 3 PART 1](https://github.com/user-attachments/assets/15672d9f-1b49-4747-bf9b-c988820fc169)

---
The SQL query retrieves the rows from the "challenge" table where the respondents report "Communication Skills" as a valuable skill and have less than 1 year of experience. Here's how it works:

1. **SELECT *:** This command tells the database to fetch all columns from the rows that match the specified conditions.

2. **FROM challenge:** tells what table to retrieve the data from, which in this case is named "challenge."

3. **WHERE Valuable_skill LIKE "%communication%":** This condition filters the rows based on the "Valuable_skill" column. WE use the `LIKE` operator with the `%communication%` pattern to find any rows where "communication" appears anywhere within the text of that column. The `%` symbols are wildcards that allow for any text before or after "communication."

4. **AND Experience = "less than a year":** This condition further filters the results by ensuring that the "Experience" column matches exactly the value "less than a year."



## DAY THREE PART 2
**QUESTION** : Create a Column That Categorizes Respondents Based on Their Years of Experience

---
```sql
UPDATE challenge
SET experience_category = 
  CASE
     WHEN Experience = "less than a year" THEN "beginner"
     WHEN Experience = "1 - 3 years" THEN "junior"
     WHEN Experience = "3 - 5 years" THEN "experienced"
     WHEN Experience = "5+ years" THEN "advanced"
END;  
```
---
![TASK 3 PART 2](https://github.com/user-attachments/assets/91028978-0ce5-42ce-865a-56c812d9489a)

---
   First, we are modifying the database structure by adding a new column called `experience_category` to the `challenge` table. This new column will  store values that represent different levels of experience, such as "beginner," "junior," "experienced," or "advanced."
   
   Next, we update the newly added column (`experience_category`) by using a `CASE` statement. This statement checks the existing `Experience` column for each row and assigns a category based on the value in that column. 
   
   - If a respondent has "less than a year" of experience, they are categorized as a "beginner."
   - If a respondent has between "1 - 3 years" of experience, they are categorized as "junior."
   - If a respondent has "3 - 5 years" of experience, they are categorized as "experienced."
   - If a respondent has "5+ years" of experience, they are categorized as "advanced."



### ASSIGNMENT
IN THE GROUP CHAT TELL US WHAT FUNCTION IS SYNONYMOUS WITH THE CASE FUNCTION IN DAX
