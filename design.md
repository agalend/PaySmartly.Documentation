
# Table of contents

# 1. Motivation

This solution has one main purpose - it should show you how I think, approach a task and give you a basic overview of my technical skills. 
I have tried to scratch an end to end solution instead of deep diving into particular modules, so that you can have a full understanding
regarding my software development life cycle comprehension.

Please, keep in mind that I was not able to tailor each and every module since I had to finish the task in a reasonable time frame.

# 2. Assumptions

First, I want to notice that I have no payroll experience whatsoever. As you can imagine the closest touch I have to payroll is while I get my salary. That's why I had done the following research:

 - I checked https://www.employment.govt.nz/ and https://www.employment.govt.nz/hours-and-wages/pay/payslip/ in order to find out the base payroll's ingredients. It turned out that it is a much complex topic than I expected. However, I was able to get the very initial impression of what is the payroll process.

 - I checked several online calculators in order to see what input data they require. I have been also using them in order to validate my     solution.

 - One interesting think I noticed while I was playing with those calculators was that they calculated the net income a little bit differently:

    netIncome = grossIncome - incomeTax - super

    However, I stuck to your task description and calculated the net income according to your expectations. However, you can see a comment reflecting this difference: [source code](https://github.com/agalend/PaySmartly.Calculations/blob/master/PaySmartly.Calculations/Calculations/Formulas.cs)

 - I also extended the task so that I can include all important topics. You might find some features awkward, however, I added them in order to give myself enough context to show everything I want.

# 3. Architecture

I am going to present you 3 different possible architectures. Keep in mind that I am going to implement the third one, microservices architecture. In addition, I will present you horizontally scaled backends in all 3 approaches. 

## 3.1. pure front-end solution

Reading the task I cannot see a hard requirement for any particular backend components apart of service(s) which servers a static content (html/css/javascript). Calculations can be done entirely into the javascript since there is no persistence requirement. Furthermore, it can be used an advanced front-end framework, such as react native, in order to provide best UI experience to both, browser, mobile and desktop clients. Blazor can be considered too:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/front-end-architecture.png">

## 3.2. three tier solution

If we want to persist some data then we cannot use the previous solution. One option is to use the old, well-known three tier architecture. If developers keep a good code quality and do not introduce a complex state then this solution can even scale out:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/3-tier-architecture.png">

## 3.3. microservices solution

Third option is to create a modern, microservices architecture:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/microservices-architecture.png">

# 4. Microservices solution

We are going to implement 7 different services in order to divide the complex logic into more granular micro services. The aim here is to be able to achieve the following goals:

   - horizontal scaling
   - fault tolerance
   - high availability

This is the summery of all 7 services:

   - api gateway -> will play role of reverse proxy and load balancer. It will route requests to the static content services, calculation services and archive services, [source code](https://github.com/agalend/PaySmartly.ApiGateway)
   - static content service -> will serve the UI, [source code](https://github.com/agalend/PaySmartly.UI)
   - calculations service -> will calculate pay slips and store them into a database,[source code](https://github.com/agalend/PaySmartly.Calculations)
   - archive service -> will request already calculated pay slip records from the database, [source code](https://github.com/agalend/PaySmartly.Archive)
   - persistence load balancer -> will route requests to many persistence services, [source code](https://github.com/agalend/PaySmartly.Persistence.LoadBalancer)
   - persistence service -> will hide the complex database logic and act as an intermediate, [source code](https://github.com/agalend/PaySmartly.Persistence)
   - legislation service -> will incorporate the complex legislation logic, such as serving a taxable income table, [source code](https://github.com/agalend/PaySmartly.Legislation)

## 4.1 technology stack

I am going to use the following technologies:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/technology-stack.png">

## 4.2 business logic

### 4.2.1 UI

### 4.2.2 Calculations

### 4.2.3 Archive

### 4.2.4 Legislation

### 4.2.5 Persistence

# 5. high availability

# 6. Api documentation

# 7. Testing

## 7.1 unit tests

## 7.2 integration tests

## 7.3 performance tests

## 7.4 load tests

## 7.5 stress tests

## 7.6 end-to-end tests

### 7.7.1 automatic tests

### 7.7.2 manual tests

# 8. CI/CD

# 9. Security

## 9.1 https

## 9.2 OAuth 2.0

# 10. Support