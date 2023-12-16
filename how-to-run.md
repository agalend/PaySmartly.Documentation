# Table of Contents

- Requirements
- Code repositories
- Download and run the docker-compose.yml
- DockerHub
- Docker container statuses
- Test

# 1. Requirements

I have created a docker compose file in order to ease the testing procedure on your local machine. You have to install:

* docker daemon, such as Docker Desktop
* set up a WSL 2 based engine, since all docker images are linux based

# 2. Code repositories

All code repositories are in GitHub: [repositories](https://github.com/agalend?tab=repositories) 

# 3. Download and run the docker-compose.yml

You can clone, download or even copy/paste the docker-compose.yml on your local machine from [here](https://github.com/agalend/PaySmartly.Deployment/blob/main/docker-compose.yml)

First ensure that the following local ports are free to use: [9080- 9091]

Then you should open a cmd, cd to the folder containing docker-compose.yml and execute the following command: `docker compose up --build`

# 4. DockerHub

All docker images are located [here](https://hub.docker.com/repositories/agalend)

# 5. Docker containers' statuses

check the docker containers' statuses once you have run the docker compose file:

<img src="https://github.com/agalend/PaySmartly.Documentation/blob/main/resources/run/running-docker-containers.png">

# 6. Test

Open you browser and load http://localhost:9080

then you can refer to [how to test](https://github.com/agalend/PaySmartly.Documentation/blob/main/how-to-test.md) 


