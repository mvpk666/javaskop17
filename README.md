Dockerized Spring Boot app in AWS Elastic Beanstalk
============================================

This is an example how to configure Dockerrun.aws.json for running Spring Boot app in AWS Elastic Beanstalk.
The application is generated with [JHipster](https://jhipster.github.io/)

Prerequisites
-------------

- JDK 1.8
- Maven 3.0+
- Docker
- [AWS account](https://aws.amazon.com/free/) (don't worry, the stuff will be doing in this example is eligible for **free tier**, that is you don't need to pay for this)
- [AWS EB CLI](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3.html)
- [EB CLI](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html)


Build project and Docker image
------------------

Build the maven project and Docker image  
```mvn clean package -Pprod docker:build```

Run application locally with **docker-compose**  
```docker-compose -f src/main/docker/app.yml up```

Stop docker-compose  
```type Ctrl+C```

Tag build image to push to AWS repo URI  
```docker tag jhipsta-app:latest YOUR_AWS_ID.dkr.ecr.YOUR_AWS_REGION.amazonaws.com/jhipsta-app:latest```

Get login command for AWS ECR  
```aws ecr get-login --region YOUR_AWS_REGION```  
This will generate docker login command that you need then to run

Push image to ECR  
```docker push YOUR_AWS_ID.dkr.ecr.YOUR_AWS_REGION.amazonaws.com/jhipsta-app:latest```

Setup ElasticBeanstalk application and environment
==================================================

Initialize AWS ElasticBeanstalk application  
```eb init```  
and go with defaults

Create environment  
```eb create```  
and go with defaults

Running application
===============

Update Dockerrun.aws.json and deploy the app.  
Run this from directory with Dockerrun.aws.json  
```eb deploy```

Run application locally with EB CLI  
```eb local run```

Automated deployment
====================

Please check [my blog post](https://medium.com/@pavelbely/deploying-dockerized-multi-container-application-to-aws-using-jenkins-833a998ce6ed#.9s8ghxcn4) on this