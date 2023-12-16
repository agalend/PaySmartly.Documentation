
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

I am going to present you 3 different possible architectures. Keep in mind that I implemented the third one, microservices architecture. In addition, I will present you horizontally scaled backends in all 3 approaches. 

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

I implemented 7 different services in order to divide the complex logic into more granular micro services. The aim here is to be able to achieve the following goals:

   - horizontal scaling
   - fault tolerance
   - high availability

This is the summery of all 7 services:

   - calculations service -> calculates pay slips and store them into a database: [source code](https://github.com/agalend/PaySmartly.Calculations/tree/master/PaySmartly.Calculations)
   - archive service -> requests already calculated pay slip records from the database: [source code](https://github.com/agalend/PaySmartly.Archive)
   - persistence service -> hides the complex database logic and act as an intermediate: [source code](https://github.com/agalend/PaySmartly.Persistence)
   - api gateway -> plays role of reverse proxy and load balancer. It routes requests to the static content services, calculation services and archive services: [source code](https://github.com/agalend/PaySmartly.ApiGateway)
   - persistence load balancer -> routes requests to many persistence services: [source code](https://github.com/agalend/PaySmartly.Persistence.LoadBalancer)
   - legislation service -> incorporates the complex legislation logic, such as serving a taxable income table: [source code](https://github.com/agalend/PaySmartly.Legislation)
   - static content service -> serves the UI: [source code](https://github.com/agalend/PaySmartly.UI)

## 4.1 technology stack

I use the following technologies:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/technology-stack.png">

## 4.2 business logic

There are 5 modules that contain business specific logic:

### 4.2.1 UI

UI is separated into 2 pages

   - calculator -> You can fill a pay slip data and get calculated pay slip:

   <img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/calculator-page.png">

   - history -> you can get pay slip records filtered by name, super rate and annual salary. I have also implemented pagination, and therefore, user can see next and previous 10 rows

   <img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/history-page.png">

### 4.2.2 Calculations

Calculations logic calculates the pay slip based on a given data. It has a dependency on the legislation service and retrieves the taxable income table. Calculations service also persist each and every pay slip, and therefore, it has dependency on the persistence service as well.

### 4.2.3 Archive

Archive logic retrieves pay slip records, and therefore, it has dependency on the persistence service as well.

### 4.2.4 Legislation

Legislation logic provides the taxable income table.

### 4.2.5 Persistence

Persistence logic add, delete, and retrieves pay slip records. It deals with mongo specific API.

# 5. high availability

These are the services that have multiple instances:

   - 2 static content services
   - 2 calculations services
   - 2 archive services
   - 3 persistence services

It is extremely easy to increase the number of those service instances, if you want.

There is:

   - 1 legislation service -> I set up only one so that I can show you a single point of failure service. If this service crash then the entire 
   calculator page will be unresponsive. 
   - 1 API Gateway -> while this can be considered as a single point of failure service too, we can mitigated this problem by introducing a leading api gateway instance and 1 or more failover gateway instances. 
   - 1 load balancer instance -> same as api gateway

While we can extend the existing architecture to reflect above limitations, 1 big issue remains - we can set the number of services only on design phase, not at runtime. This has many limitations such as:

   - if all service instances break then part of the functionality will stop working
   - if the system encounters intensive load then it can become unresponsive
   - the system will consume resources (money in the cloud) during the quiet hours  

Above limitations can be mitigated if we introduce a container orchestrator, such as K8S. I have created a docker image for each and every service, and therefore, the entire solution is prepared for introducing the container orchestrator.

# 6. Api documentation

There are OpenApi support and swagger interface for:

   - calculations rest api:

   <img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/swagger-calculations.png">

   - archive rest api

   <img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/swagger-archive.png">

# 7. Security

## 7.1 https

I have been using http in order to ease the development, however, https is the must protocol for production. It must be used between the client apps and the api gateway at least. If we use some kind of private network behind the api gateway than we can consider using http into it, however, each and every connection outside this private network must go through https.

## 7.2 OAuth 2.0

I have not implemented any authentication and authorization, however, in most cases this is a must requirement for production. One possible solution is to use some auth provider which implement OAuth 2.0, such as auth0:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/security-architecture.png">

# 8. Support

All .NET services, including the api gateway and persistence load balancer, have OpenTelemetry support. That way we can send metrics, traces and logs to a server, such as Prometheus, and visualize them using some tool, such as Grafana. I have implemented just console exporter:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/design/open-telemetry-console.png">

# 9. CI/CD

due to the time limitation I was not able to create a CI/CD pipeline. One possible option is to use github actions in order to build, test and deploy all services.

# 10. Testing

Testing is an critical part of any production ready system, however, due to the time limitation I was not able to create all necessary tests:

## 10.1 unit tests

I have created tests for the calculations service, you can see the implementation here: [source code](https://github.com/agalend/PaySmartly.Calculations/tree/master/PaySmartly.Calculations.Tests)

I added a git hook as well: [source code](https://github.com/agalend/PaySmartly.Calculations/blob/master/git-hooks/pre-commit)

## 10.2 integration tests

TBD, one possible solution can be using of github actions

## 10.3 performance tests

TBD

## 10.4 load tests

TBD

## 10.5 stress tests

TBD

## 10.6 end-to-end tests

TBD

### 10.10.1 automatic tests

TBD

### 10.10.2 manual tests

TBD