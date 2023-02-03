# Health Tracker Database
A database designed to help users efficiently manage their health history data. The database contains information on water intake, weight, exercise, and meal history.

## Getting Started
This database was built using SQLite3. The .txt files in this repository contain the SQL statements to recreate the database file, create the tables, populate the tables, and select data from the tables. The SQL statements can be copy/pasted directly into your sqlite3.exe.

## Database Requirements
This database is designed to allow users to input their daily exercise, meals, weight, and water intake. Each user is identified by their unique username and ID. The database contains the following data:

* Water intake history that tracks the ounces of water consumed by a user on a particular day.
* Weight history that tracks the user's weight in pounds on a particular day.
* Exercise history that tracks the user's workout on a particular day, including the exercise name, number of sets, number of reps, and weight (if applicable).
* Meal history that tracks what the user is eating on a particular day, including calories, amount of carbohydrates, amount of fats, amount of proteins, food name, timestamp, and date.
* The total ounces of water consumed by a user on a given date.
## Database Relations
The database relations are in BCNF and each relation has only one functional dependency.

## Example Queries
```SQL

/* Returns the max weight for each exercise, and when that max was achieved for a particular user. 
   In this case, the user is ‘ILoveBamboo.’ */
select Date, Exercise_Name, max(Weight) as Max_Weight
from EXERCISE_HISTORY
where User_Id = (select Id from USER where Username = 'ILoveBamboo')
group by Exercise_Name;

/* Calculates the total grams of protein a user consumed on a specified day. 
   In this case, the user is ‘ILovePandas.’ Protein can be substituted with any other nutrient to find that nutrient’s total as well. */
select sum(protein)
from MEAL_HISTORY
where User_Id = (select Id from USER where Username = 'ILovePandas') and Date = date('now', '-2 day');
```

## Entity Relationship Diagram
![image](https://user-images.githubusercontent.com/76570188/192075481-fc5aaa71-a20b-4d03-8731-02363dd293cd.png)
