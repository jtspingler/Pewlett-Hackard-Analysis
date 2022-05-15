# Pewlett-Hackard-Analysis

Employee database analysis on retiring employees using SQL and pgAdmin

## Overview

The purpose of this project was to analyze the data at Pewlett-Hackard (PW) and identify the quantity of employees that are going to retire. By getting this data we were able to project hiring needs and what the retirement packages will look like for the folks who qualify.

- Software Used:
  - SQL
  - PostgreSQL
  - pgAdmin

## Results
- By joining the employees and titles table, I was able to filter by birth date and after removing duplicates I found that there are 90,398 who are going to retire. That is a significant number!

[unique_titles.csv](https://github.com/jtspingler/Pewlett-Hackard-Analysis/blob/main/Data/unique_titles.csv)

- Breakdown of employees leaving by department: 29,414 Senior Engineers, 28,254 Senior Staff, 14,222 Engineers, 12,243 Staff, 4,502 Technique Leaders, 1,761 Assistant Engineers, and 2 Managers. 

![unique_titles_pic](https://github.com/jtspingler/Pewlett-Hackard-Analysis/blob/main/unique_titles_pic.PNG)

-By joining the employees, department employees, and the titles tab I was able to create the mentorship eligibility table which will allow for PH to plan accordingly for the mentorship package.

[mentorship_eligibility.csv](https://github.com/jtspingler/Pewlett-Hackard-Analysis/blob/main/Data/mentorship_eligibilty.csv)

- Breakdown of eligible employees: 402 Engineers, 392 Senior Staff, 332 Staff, 290 Senior Engineers, 77 Technique Leaders, and 56 Assistant Engineers. 

![mentorship_eligibility_pic](https://github.com/jtspingler/Pewlett-Hackard-Analysis/blob/main/mentorship_eligibility_pic.PNG)

[title_mentorship_eligibility.csv](https://github.com/jtspingler/Pewlett-Hackard-Analysis/blob/main/Data/mentorship_eligibilty.csv)

### Summary of Results
- A total of 90,398 employees are of retirement-age.
- Almost 95% of the retiring population have "Engineer" or "Staff" in their title.
- 1,940 employees are eligible to be mentors
- There is roughly 1 mentor for each 45 vacancies.

- I’d like to have a relative understanding of the percentage of people leaving the company. To do this we need to gain a better understanding of the total population at PH. Here's a query I would use to extract that information: 

```
SELECT DISTINCT ON (employees.emp_no) employees.emp_no,
    employees.first_name,
    employees.last_name,
    titles.title,
    titles.from_date,
    titles.to_date
INTO all_employees
FROM employees
LEFT JOIN titles
ON employees.emp_no = titles.emp_no
ORDER BY employees.emp_no, titles.to_date DESC

SELECT COUNT (emp_no)
FROM all_employees
```
- From this query we get 300,024 total employees. Since almost a third of the company will be retiring and there are not enough mentors to meet the number of vacancies, I would recommend expanding the mentorship program in order to get more mentors.
