---
layout:     post
title:      Availability and Scalability for Microservice-Based Order Delivery System
subtitle:   
date:       2020-08-10
author:     Borong
header-img: img/post-bg-iWatch.jpg
catalog: true
tags:
    - Microservice
    - Domain Driven Design
    - Microsoft Azure
---

## OVerview

First, the system should have high availability because some restaurants may provide special offer during some Festivals, such as Christmas day and national day. Then many customers may access the web pages and order food in the same period. So the system need to handle a large amount of load. Next, it should be able to scale automatically to save some expense for web server.

## Availability

#### Microservice

Microservice architecture – a variant of the service-oriented architecture (SOA) structural style – arranges an application as a collection of loosely coupled services. In a microservices architecture, services are fine-grained and the protocols are lightweight.[(Wikipeda)](https://en.wikipedia.org/wiki/Microservices)

Microservice-based distributed system can significantly increase the availability of the back-end. For example, if a customer wants to check menu and make an order by the system. The request from front-end will first approach the gateway. Then, gateway will invoke client feign, which is also a microservice, then the client feign will call menu and order services to get and save data. The two services can run independently, so that can improve the availability.

#### Load Balancer

the Azure Spring Cloud makes it easy to add a load balancer in each layer. For example, when I
increase the instances for all microservices, it will automatically distribute the load. According to the solution provided by the Azure document, we tried several solutions to add a load balancer, including Azure Traffic Manager, Azure front door, and load balancer. We finally chose the Azure Spring Cloud default load balancer because the first two solutions have some obvious shortcomings. AzureTraffic Manager is more expensive. Specifically, it can only be integrated into the costive Standard plan for Azure Spring Cloud. In addition, the stress test results of the load balancer are better than the Azure front door. In addition, Azure Traffic Manager and Azure front door require more public endpoints. For example, a system with 10 microservices requires 10 public endpoints to implement load balancers. However, the previewed Azure Spring Cloud currently provides five ones. In contrast, the default load balancer only needs a public endpoint of a gateway. It is a better solution for the project.

#### Azure Redis Cache

Azure Redis Cache is fully managed, open source–compatible in-memory data store to power fast, scalable applications. [(Azure Redis Cache)](https://azure.microsoft.com/en-us/services/cache/)

### Scalability

With Azure Portal, I can scale up and scale out all microservices manually and automatically, such as increasing the number of instance, CPU cores, memory for each microservice. More details are shown below in the two pictures.

![alt text](https://raw.githubusercontent.com/grass-mudhorse/grass-mudhorse.github.io/master/img/scalable1.png)


![alt text](https://raw.githubusercontent.com/grass-mudhorse/grass-mudhorse.github.io/master/img/scalable2.png)

The Auto Scale function will help to adapt the availability of the system. It would save expense for the Azure Server.

### Conclusion

The article lists some solutions for availability and scalability for the order delivery system design. In order to evaluate the performance for these solutions, a technical evaluation is necessary. More details related to load testing will be posted later for discussion. Also,Some solutions for the recommender system will be discussed in another post later.



