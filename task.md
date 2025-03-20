# Task

When supplied employee details: first name, last name, annual salary (positive integer) and super rate (0% - 50% inclusive), pay period, the program should generate pay slip information with name, pay period, gross income, income tax, net income and super.

The calculation details will be the following:

   - pay period = per calendar month
   - gross income = annual salary / 12 months
   - income tax = based on the tax table provided below
   - net income = gross income - income tax
   - super = gross income x super rate

For example, the payment in March for an employee with an annual salary of $60,050 and a super rate of 9% is:

   - pay period = Month of March (01 March to 31 March)
   - gross income = 60,050 / 12 = 5,004.17
   - income tax = (14000 * 0.105 + 34000 * 0.175 + 12050 * 0.3) / 12 = 919.58
   - net income = 5,004.17 – 919.58 = 4,084.59
   - super = 5,004.17 x 9% = 450.38

Example input/output:

Input (first name, last name, annual salary, super rate (%), pay period):

John,Smith,60050,9%,March
Alex,Wong,120000,10%,March

Output (name, pay period, gross income, income tax, net income, super):

John Smith,01 March – 31 March,5004.17,919.58,4084.59,450.38
Alex Wong,01 March – 31 March,10000.00,2543.33,7456.67,1000.00

As part of the solution:

   - List any assumptions that you made in order to solve this problem.
   - Provide instructions on how to run the application.
   - Include a simple web interface with input fields and display of the output