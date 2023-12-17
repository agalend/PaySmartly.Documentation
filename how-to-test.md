# Table of Contents

- Calculator page
- History page
- Killing random services
- Swagger

# 1. Calculator page

You can calculate a pay slip following these steps (all inputs are required):

- first you should fill: First Name, Last Name, Annual Salary, Super Rate and Month
- then you should click on Calculate button
- finally you will see the calculated pay slip data on the right:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/test/calculator-page.png">

# 2. History page

You can request pay slip records following these steps (all inputs are required):

- first you should filter by one of these: 
    - name -> you should fill first and last name
    - super rate -> fill the desired rate range, for example from 7 to 9
    - annual salary -> fill the desired salary range, for example from 60050 to 12000
- then you should click on Request Data button
- finally bellow table will be populated, if any records exist:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/test/history-page.png">

# 3. Killing random services

You can kill some service instance, such as calculations one. You should be able to perform pay slip calculations after killing it since I have set up 2 instances. If you kill the second one too then you will encounter error:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/test/error-page.png">

However, you should still be able to retrieve pay slip records since history page do not request a calculations service instance at all.

You can run one of the two calculations instances, then refresh in order to load the calculator page again and you should be able to perform pay slip calculations again. You can killing and running again calculations, archive and persistence instances in order to test the failover mechanism. API Gateway, persistance load balancer and legislation instances are single point of failure right now.

# 3. Swagger

you can request calculations' swagger page: [http://localhost:9080/api/calculations/swagger/index.html](http://localhost:9080/api/calculations/swagger/index.html)

you can request archive's swagger page: [http://localhost:9080/api/archive/swagger/index.html](http://localhost:9080/api/archive/swagger/index.html)



