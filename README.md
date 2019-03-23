# COEN241-Kubernerds
### Evaluation of deployment patterns of microservices

We used the following open source microservice applications for evaluating various deployment pattern.

Sock Application → https://microservices-demo.github.io/

FoodToGo → https://github.com/microservices-patterns/ftgo-application

Clone the above repositories, and make configuration changes to deploy them using various patterns:

## Language specific format
To run Frontend service
Install git
```
git clone https://github.com/microservices-demo/front-end.git
cd front-end
```
Install node, yarn
```
yarn install
```
Run node
```
npm start
```
Go to http://localhost:8079/index.html

## Service per VM
#### To run Frontend service
Install git
```
git clone https://github.com/microservices-demo/front-end.git
cd front-end
```
Install node, yarn
```
yarn install
```
#### To run User service
```
git clone https://github.com/microservices-demo/user.git
cd user
```
Install go, glide, mongo
```
cd go/src/github.com/microservices-demo/user
./user -port=8080 -database=mongodb -mongo-host=localhost:27017
```
## Service per Container
Install git
```
git clone https://github.com/microservices-demo/microservices-demo
cd microservices-demo
```
Install docker, docker-compose
```
docker-compose -f deploy/docker-compose/docker-compose.yml up -d
```
### Service per pod using Kubernetes
Install git
```
git clone https://github.com/microservices-demo/microservices-demo
cd microservices-demo/deploy/kubernetes
```
Install kubectl
```
kubectl create namespace sock-shop
kubectl apply -f complete-demo.yaml
```
## Serverless Deployment
Install git
Install gradle 
```
git clone https://github.com/microservices-patterns/ftgo-application
cd ftgo-application-master  
cd ftgo-application-master\ftgo-restaurant-service-aws-lambda
```
Run gradle.scripts to build the application which creates a zip folder 
```
task buildZip(type: Zip) {
from compileJava
from processResources
into('lib') {
from configurations.runtime
    }
}
```
Modify the serverless.yml file as follows:
```
provider:
  name: aws
  runtime: java8
  timeout: 35
  region: us-west-2
  stage: dev
  environment:
    SPRING_DATASOURCE_DRIVER_CLASS_NAME: com.mysql.jdbc.Driver
    SPRING_DATASOURCE_URL: jdbc:mysql://192.168.99.100//eventuate
    SPRING_DATASOURCE_USERNAME: mysqluser
    SPRING_DATASOURCE_PASSWORD: mysqlpw
```
After modifying deploy the file using following command:
```
serverless deploy
```
## Load test microservices using Locust
```
docker run --net=host weaveworksdemos/load-test -h <ip>:<port>/<url> -r 500 -c 2
```
