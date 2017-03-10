Dockerized Spring Boot app in AWS Elastic Beanstalk
============================================

This is an example how to configure Dockerrun.aws.json for running Spring Boot app in AWS Elastic Beanstalk.
The application is generated with [JHipster](https://jhipster.github.io/)

Prerequisites
-------------

- JDK 1.8
- Maven 3.0+
- Docker
- [AWS EB CLI](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html)
- [AWS account](https://aws.amazon.com/free/) (don't worry, the stuff will be doing in this example is eligible for **free tier**, that is you don't need to pay for this)


Steps to to deploy
------------------

Build the maven project and Docker image  
```mvn clean package -Pprod docker:build```

Run application locally with **docker-compose**  
```docker-compose -f src/main/docker/app.yml up```

Stop docker-compose  
```type Ctrl+C```

Tag build image to push to AWS repo URI  
```docker tag jhipsta-app:latest 740192421584.dkr.ecr.eu-west-1.amazonaws.com/jhipsta-app:latest```

Get login command for AWS ECR  
```aws ecr get-login --region eu-west-1```  
This will generate docker login command that you need then to run

Push image to ECR  
```docker push 740192421584.dkr.ecr.eu-west-1.amazonaws.com/jhipsta-app:latest```

Deploy the app (Run it from directory with Dockerrun.aws.json)  
```eb deploy```

Run application locally with EB CLI
```eb local run```