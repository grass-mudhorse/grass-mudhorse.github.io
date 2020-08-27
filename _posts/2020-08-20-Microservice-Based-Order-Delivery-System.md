---
layout:     post
title:      Microservice-Based Order Delivery System Design
subtitle:   
date:       2020-08-05
author:     Borong
header-img: img/post-bg-iWatch.jpg
catalog: true
tags:
    - Microservice
    - Domain Driven Design
    - Microsoft Azure
---


## Overview

I led a group of five people to develop the master's final project with Microsoft sponsorship. The project is a microservice-based system implemented by Java Spring Boot and Spring Cloud framework. The system is based on Domain-driven design, witch has four layers. More details are as follows.

## Project Objective

There are two main issues that we concerned about in Covid-19 situation.

For customers, how to enjoy a tasty meal from a restaurant conveniently in the Covid-19 situation? For restaurants, how to keep the business running well and extend the service area under the Covid-19 restriction?

First, it should have high availability because some restaurants may provide special offer during some Festivals, such as Christmas day and national day. Then many customers may access the web pages and order food in the same period. So the system need to handle a large amount of load. Next, it should be able to scale automatically to save some expense for web server. Also, it should have excellent UI and provide personalized recommendations to attract more regular customers. Finally, it should have excellent Functionality for both customer and restaurant roles. Specifically, for customers, they should be able to login, check information of restaurants and menus, then order some dishes. For restaurants, they should be able to login, update menus and handle orders.

## Domain-driven design

Domain-driven design (DDD) is the concept that the structure and language of software code (class names, class methods, class variables) should match the business domain. For example, if a software processes loan applications, it might have classes such as LoanApplication and Customer, and methods such as AcceptOffer and Withdraw.[Wikipeda](https://en.wikipedia.org/wiki/Domain-driven_design)

![](https://ws4.sinaimg.cn/large/006tKfTcgy1fhg20ydk8uj30go0brwh1.jpg)

## Layers
A basic DDD system should have four layers.

1. **Presentation Layer**: Provides an interface to the user. Uses the Application Layer to achieve user interactions.
2. **Application Layer**: Mediates between the Presentation and Domain Layers. Orchestrates business objects to perform specific application tasks. Implements use cases as the application logic.
3. **Domain Layer**: Includes business objects and the core (domain) business rules. This is the heart of the application.
4. **Infrastructure Layer**: Provides generic technical capabilities that support higher layers mostly using 3rd-party libraries.

![](https://github.com/grass-mudhorse/grass-mudhorse.github.io/blob/master/img/structure.png)

In the access layer, there are a gateway and web pages, which handle access from users. In application layer, there are three Feign Client based on three types of users. It makes build web service clients easier. In domain layers, there are six data-driven microservices, they handle the requests from application layer and
interact with database. In infrastructure layer, there are some database mapping tool to connect domain layer and MySql database.

## Technical Challenges

As the targets shown above, we face some difficult challenges to build a high availability and scalability system. Also, the recommender service integrated in the project is another critical challenge to attract more regular customers. More details will be discussed in another post later.

