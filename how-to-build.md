# Table of Contents

- Building all .NET services
- Building the react app
- Run all services and test

# 1. Building .NET services

I have used a minimal api and grpc. If you have access to the public nuget repository then you should be able to build and run each and every C# repository right away. You have to have .NET8 installed.

# 2. Building the react app

I have crated a react app and added 2 additional dependencies: axios and react-bootstrap. If you have access to the public npm registry then you should be able to install, build and run this react app right away.

# 3. Run all services and test

First you should either instal mongodb locally or run a mongodb docker container exposing port 27017.

Then you can clone, build and run each and every service:

   - legislation service -> incorporates the complex legislation logic, such as serving a taxable income table: [source code](https://github.com/agalend/PaySmartly.Legislation)
   - calculations service -> calculates pay slips and store them into a database: [source code](https://github.com/agalend/PaySmartly.Calculations)
   - archive service -> requests already calculated pay slip records from the database: [source code](https://github.com/agalend/PaySmartly.Archive)
   - persistence service -> hides the complex database logic and act as an intermediate: [source code](https://github.com/agalend/PaySmartly.Persistence)
   - static content service -> serves the UI: [source code](https://github.com/agalend/PaySmartly.UI)
   - api gateway -> plays role of reverse proxy and load balancer. It routes requests to the static content services, calculation services and archive services: [source code](https://github.com/agalend/PaySmartly.ApiGateway)
   - persistence load balancer -> routes requests to many persistence services: [source code](https://github.com/agalend/PaySmartly.Persistence.LoadBalancer)

Then you can just open your browser and load http://localhost:9080 and start debugging.