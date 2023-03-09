his problem set consists of two data modeling scenarios. You will be asked to analyze the strengths and weaknesses of some design alternatives for each scenario. Short answers are fine – one or two paragraphs per question
would be an appropriate length.
Scenario I In this scenario, we are interested in modeling student enrollment in Stanford courses. We would like to
answer questions such as:
• Which courses are most popular? Which instructors are most popular?
• Which courses are most popular among graduate students? Undergraduates? • Are there courses for which the
assigned classrooms is too large or too small?
We are planning to have a course enrollment fact table with the grain of one row per student per course enrollment.
In other words, if a student enrolls in 5 courses there will be 5 rows for that student in the fact table. We will use the
following dimensions: Course, Department, Student, Term, Classroom, and Instructor. There will be a single fact
measurement column, EnrollmentCount. Its value will always be equal to 1.
We are considering several options for dealing with the Instructor dimension. Interesting attributes of instructors
include FirstName, LastName, Title (e.g. Assistant Professor), Department, and TenuredFlag. The difficulty is that a
few courses (less than 5%) have multiple instructors. Thus it appears we cannot include the Instructor dimension in
the fact table because it doesn’t match the intended grain. Here are the options under consideration:
OptionA
Option B
Option C
ModifytheInstructordimensionbyaddingspecialrowsrepresentinginstructorteams.Forexample,CS276ais taught by
Manning and Raghavan, so there will be an Instructor row representing “Manning/Raghavan” (as well as separate
rows for Manning and Raghavan, assuming that they sometimes teach courses as sole instructors). In this way, the
Instructor dimension becomes true to the grain and we can include it in the fact table.
Change the grain of the fact table to be one row per student enrollment per course per instructor. For example, there
will be two fact rows for each student enrolled in CS 276a, one that points to Manning as an instructor and one that
points to Raghavan. However, each of the two rows will have a value of 0.5 in the EnrollmentCount field instead of
a value of 1, in order to allow the fact to aggregate properly. (Enrollments are “allocated” equally among the
multiple instructors.)
Create two fact tables. The first has the grain of one row per student enrollment per course and doesn’t include the
Instructor dimension. The second has the grain of one row per student enrollment per course per instructor and
includes the Instructor dimension (as well as all the other dimensions). Unlike Option B, the value of
EnrollmentCount will be 1 for all rows in the second fact. Tell warehouse users to use the second fact table for
queries involving attributes of the instructor dimension and the first fact table for all other queries.

Please answer the following questions.
Question 1. What are the strengths and weaknesses of each option?
Question 2. Which option would you choose and why?
Question 3. Would your answer to Question 2 be different if the majority of classes had multiple instructors? How
about if only one or two classes had multiple instructors? (Explain your answer.)
Question 4. [OPTIONAL] Can you think of another reasonable alternative design besides Options A, B, and C? If
so, what are the advantages and disadvantages of your alternative design?

ANS : 1. Option A:
Strengths: It keeps the Instructor dimension at the grain of the fact table. It allows for individual instructors as well as instructor teams to be included. 
It can simplify the fact table and prevent sparse data.
Weaknesses: It can be complex to maintain and result in redundant data, especially if multiple courses have instructors in common. It may not be 
easy to query for individual instructors if they are grouped in teams.

Option B:
Strengths: It includes the Instructor dimension at the grain of the fact table. It provides accurate enrollment counts for courses with multiple instructors. 
It can simplify queries involving the Instructor dimension.
Weaknesses: It can result in a larger fact table and complicate the allocation of enrollment counts among multiple instructors. It may lead to sparse data
 if only a small number of courses have multiple instructors.

Option C:
Strengths: It can optimize query performance by having separate fact tables. It provides accurate enrollment counts for individual instructors. It can 
prevent sparse data.
Weaknesses: It requires more storage space. It may be challenging to maintain consistency between the two tables, especially if there are frequent 
updates to the data.

Answer 2:
The choice of which option to use depends on the specific needs of the organization. If data consistency and ease of maintenance are prioritized, 
Option A may be the best choice. If query performance is a priority, Option C could be a better option. Option B may be a reasonable compromise 
between the two, although it requires careful consideration of the trade-offs involved.

Answer 3:
If the majority of classes had multiple instructors, Option B may become more attractive as it would provide accurate enrollment counts for all instructors. 
However, if only one or two classes had multiple instructors, Option A could still be a viable solution, as it would prevent sparse data and maintain consistency 
with the rest of the fact table.

Answer 4:
Another reasonable alternative design could be to create a separate fact table for courses with multiple instructors, rather than including the Instructor 
dimension in the same fact table. This would avoid the issues of sparse data and complicated allocation of enrollment counts, while still providing accurate 
enrollment information for courses with multiple instructors. However, this would require additional maintenance and querying across multiple fact tables.

-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Scenario II In this scenario, we are building a data warehouse for an online brokerage company. The company
makes money by charging commissions when customers buy and sell stocks. We are planning to have a Trades fact
table with the grain of one row per stock trade. We will use the following dimensions: Date, Customer, Account,
Security (i.e. which stock was traded), and TradeType.
The company’s data analysts have told us that they have developed two customer scoring techniques that are used
extensively in their analyses.
· Each customer is placed into one of nine Customer Activity Segments based on their frequency of
transactions, average transaction size, and recency of transactions.
· EachcustomerisassignedaCustomerProfitabilityScorebasedontheprofitsearnedasaresultofthatcustomer’s
trades. The score can be either 1,2,3,4, or 5, with 5 being the most profitable.
These two scores are frequently used as filters or grouping attributes in queries. For example:
· How many trades were placed in July by customers in each customer activity segment?
· What was the total commission earned in each quarter of 2003 on trades of IBM stock by customers
with a profitability score of 4 or 5?
There are a total of 100,000 customers, and scores are recalculated every three months. The activity level or
profitability level of some customers changes over time, and users are very interested in understanding how
and why this occurs.
We are considering several options for dealing with the customer scores:
OptionA Option B Option C
Option D
ThescoresareattributesoftheCustomerdimension.Whenscoreschange,theoldscoreisoverwrittenwiththe new score
(Type 1 Slowly Changing Dimension).
The scores are attributes of the Customer dimension. When scores change, new Customer dimension rows are
created using the updated scores (Type 2 Slowly Changing Dimension).
The scores are stored in a separate CustomerScores dimension which contains 45 rows, one for each combi- nation
of activity and profitability scores. The Trades fact table includes a foreign key to the CustomerScores dimension.
The scores are stored in a CustomerScores outrigger table which contains 45 rows. The Customer dimension
includes a foreign key to the outrigger table (but the fact table does not). When scores change, the foreign key
column in the Customer table is updated to point to the correct outrigger row.
Please answer the following questions.
Question 5. What are the strengths and weaknesses of each option?
Question 6. Which option would you choose and why?
Question 7. Would your answer to Question 6 be different if the number of customers and/or the time interval
between score recalculations was much larger or much smaller?

Answer 5:

Option A:
Strengths: Simple to implement, takes less storage space, and allows easy filtering of scores.
Weaknesses: It overwrites the old score, so there is no record of how scores change over time.

Option B:
Strengths: Keeps track of the score changes over time, and allows analysis of score changes.
Weaknesses: Increases the storage space requirements and complexity of the database, and requires additional logic to handle duplicate customer rows.

Option C:
Strengths: Separates the scores from the Customer dimension, reduces the amount of data duplication, and allows easy filtering by activity and profitability scores.
Weaknesses: Requires additional joins to retrieve the scores for analysis, and increases the complexity of the database design.

Option D:
Strengths: Similar to Option C, but stores the scores in an outrigger table, reducing the complexity of the fact table.
Weaknesses: Increases the complexity of the customer dimension and requires additional joins to retrieve the scores for analysis.

Answer 6:
I would choose Option B, which uses a Type 2 Slowly Changing Dimension to track score changes over time. While this option requires more storage space and complexity, 
it provides a complete history of customer score changes and allows for easy analysis of how scores change over time. This information can be valuable for understanding 
customer behavior and making business decisions.

Answer 7:
If the number of customers and/or the time interval between score recalculations was much larger, Option C or D may be a better choice since it separates the scores from 
the Customer dimension, reducing data duplication and making queries more efficient. On the other hand, if the number of customers and/or the time interval between score 
recalculations was much smaller, Option A may be a more viable choice since there will be less data to track and fewer score changes to record.






