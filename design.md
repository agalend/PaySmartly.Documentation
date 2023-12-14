
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

I have initially investigated 3 different approaches: 

## 3.1. pure front-end solution

Reading the task I cannot see a hard requirement for any particular backend components apart of service(s) which servers a static content (html/css/javascript). Calculations can be done entirely into the javascript since there is no persistance requirement. Furthermore, it can be used an advanced front-end framework, such as react native, in order to provide best UI experience to both, desktop and mobile clients. However, I reckon that such solution cannot be used for business needs, and therefore, I decided to create a SOA. Blazor is also an option.

<picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/front-end-architecture.png">
</picture>

## 3.2. monolithic SOA solution

## 3.3. microservices solution

# 4. Microservices solution

## 4.1 technology stack

## 4.2 teams

## 4.3 horizontal scaling

# 5. Api documentation

# 6. Testing

## 6.1 unit tests

## 6.2 integration tests

## 6.3 performance tests

## 6.4 load tests

## 6.5 stress tests

## 6.6 end-to-end tests

### 6.6.1 automatic tests

### 6.6.2 manual tests

# 7. CI/CD

# 8. Security

## 8.1 https

## 8.2 OAuth 2.0

# 9. Support