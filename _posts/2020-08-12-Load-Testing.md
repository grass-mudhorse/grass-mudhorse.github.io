---
layout:     post
title:      Stress Testing for the project on Azure Spring Cloud
subtitle:   
date:       2020-08-12
author:     Borong
header-img: img/post-bg-iWatch.jpg
catalog: true
tags:
    - Microservice
    - Microsoft Azure
    - Azure Spring Cloud
    - Load testing
---


## Overview

In order to evaluate the performance for these solutions, a technical evaluation is necessary.

## K6

k6 is a developer-centric, free and open-source load testing tool built for making performance testing a productive and enjoyable experience. Using k6, you'll be able to catch performance regression and problems earlier, allowing you to build resilient systems and robust applications.[(K6)](https://k6.io/docs/)

### Stress testing

Stress Testing is a type of load testing used to determine the limits of the system. The purpose of this test is to verify the stability and reliability of the system under extreme conditions.[(K6)](https://k6.io/docs/)

### Evaluation

I wrote script for evaluation setting, then ran it on K6 CLI. The setting of the evaluation is shown below in th picture.

![setting1](https://raw.githubusercontent.com/grass-mudhorse/Order-Delivery-System-Azure-Cloud-Final-Version/master/Load%20testing%20Script/Smoke%20testing%20and%20stress%20testing%20results/stress_test_setting.PNG)

It mainly tests the services for customers. The target number of customers is 200. The whole process is about 30 minutes, and a bunch of requests is sent every 3 seconds. It takes 9 mins to reach the normal load, 7 mins to approach the breaking point, 7 mins to exceed the breaking point.

![setting2](https://raw.githubusercontent.com/grass-mudhorse/Order-Delivery-System-Azure-Cloud-Final-Version/master/Load%20testing%20Script/Smoke%20testing%20and%20stress%20testing%20results/stress_test_setting.PNG)

The number of instance for each microservice is shown above. Because I mainly focus on the customer role, I increased the number of fundamental services, such as menu. order, account, recommendation, user services. Also, I grow the number of some microservices work as interfaces, such as gateway and clientfeign.

### System Performance

The testing result is shown below.

![](https://raw.githubusercontent.com/grass-mudhorse/grass-mudhorse.github.io/master/img/stress_testing_result.png)

According to the summary provided by K6 CLI, my computer sent 22159 sets of requests, which has five requests in one-set, to the back-end on the Azure server. On average, about 83% of requests received response successfully. The main failures were related to the login function because the process would compare the input with the customer's information stored in the database. 98% of requests such as checking the menu, recommendation inform, order details could get a response successfully. And checking order history even had a 100% success rate.

Also, Azure portal provides some visualization tool for distribution tracing, it helps us to understand the insight of the system's performance.

![](https://raw.githubusercontent.com/grass-mudhorse/Order-Delivery-System-Azure-Cloud-Final-Version/master/Load%20testing%20Script/Smoke%20testing%20and%20stress%20testing%20results/distributed%20tracing.PNG)

![](https://raw.githubusercontent.com/grass-mudhorse/Order-Delivery-System-Azure-Cloud-Final-Version/master/Load%20testing%20Script/Smoke%20testing%20and%20stress%20testing%20results/customer_stress_testing_failure.PNG)

### Conclusion

The K6 is a powerful tool for auto testing. The testing result shows the microservice-based system can handle 200 people's load in 30 mins, although there are still some bottleneck for the login function. It shows that we need to improve the process for login and give details for each service's performance. Later, the evaluation for recommender system is also essential. A hold-out testing will be discussed in another post later.



