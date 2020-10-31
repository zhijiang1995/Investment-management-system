# Investment management system

This is a investment management system. User can use this system to manage data about income, expenses and investment portfolios. And this systemcan provide a real time cost analysis information and a highly filterable activity dashboard to keep track of users account activity such as deposits, withdrawals and executed trades.

## Modules

1.**Discovery Service**

Port:8889

This module offers Service Discovery function. You can access localhost:8889 to accquire information about other instances, including name, port, status and so on. Every instance will register at localhost:8889/eureka and know the status of other instances at ，http://localhost:8889/serviceregistry/instance-status.

2.**Config Service**

Port:9990

Config Service implements external configuration. For each module listed below, if you use

    spring.cloud.config.label= master
	spring.cloud.config.profile= dev
	spring.cloud.config.discovery.enabled=true
	spring.cloud.config.discovery.service-id= configservice

in bootstrap.properties, it will get some key parameters at [ConfigOnGithub](https://github.com/PhoeniXuzoo/Microservice-based-finance-management-system/tree/master/ConfigOnGithub). if the name of a application is A, then the name of configuration file has to be A-dev.properties.

3.**Oauth2 Service**

Port:8882

Oauth2 is a protocol which allows third-party applications to grant limited access to an HTTP service. Oauth2 Service implements functions of registration, login, and authority management. There is a key topic about authority management.

if Service A wants to access the resources which belongs to Service B, A has to accquire an access code from Oauth2 Service. Some details can be found at [Spring Cloud Security](https://spring.io/projects/spring-cloud-security) and [Oauth2](https://oauth.net/2). If you do not own a right access code, your request will be blocked.

4.**APIGateway**

port:9990

APIGateway implements Routing. The routing table is:


| service-id or url| path |
| :---------- | :---------- |
| localhost:8882 | /uaa/** |
| accountservice | /accounts/** |
| incomeservice | /incomes/** |
| expenseservice | /expenses/** |
| realassetsservice | /realassets/** |
| statisticservice | /statistics/** |

There is a simple example. If a user access localhost:9990/statistics/**, then this request will be sent to Statistic Service. APIGateway can get address and port of Statistic Service from Discovery Service. If there are three instances of Statistic Service, APIGateway will adopt *Polling* strategy to implement *Load Balancing*.

Any request from users will be sent to APIGateway, and then, this service will route the request to other Services. When a service complete a task, the result of the task will be sent to APIGateway. At last, APIGateway send the response to users. For users, they do not know existence of other Services, they feel like that APIGateway deals with all of requests.

5.**Account Service**

Port:8881

This module deal with basic information about users, including name, update time, genre, age and so on. It use 3-tier architecture. The upper layer is RESTcontroller, the middle layer is Business Logic Layer, and the low-level layer is Data access layer. 

6.**Income Service**

Port:10000

This module offer the function of income management. You can create an income item with some properties, such as name, value, type, source, frequency, time point and additional information. It is also convenient for you to use a .xls file to upload a series of income data. A Pie chart and a line chart on the webpage can help you understand your structure of income. In the income table, you can search or modify or delete an income item.

7.**Expenses Service**

Port:10010

8.**Finance Product Service**

Port:10030

9.**Real Assets Service**

Port:10040

10.**Statistic Service**

Port:10050

Statistic Service use [Spring Cloud OpenFeign](https://spring.io/projects/spring-cloud-openfeign) to accquire resources from Income Service, Expenses Service, Finance Product Service, Real Assets Service, Account Service by calling their RESTful APIs. Statistic Service use data to generate a .xls file for downloading.

If there is a failure in calling RESTful APIs, Hystrix will stop the failure affecting other services. This kind of failure will not the generation process of .xls.

## Features

- SPA(Single page web application)
- Microservice-based
- Oauth2
- RESTful API
- Batch Upload and Batch Download
- Load Balancing
- Feign
- Hystrix

Each service is responsible for only one function and functions based on receiving and generatings events. Each service is independent and is not aware of its neighborhoods.
## Main Technology used in this project

<ul>
	<li>Java</li>
	<li>Spring Boot</li>
	<li>
		Spring Cloud
		<ul>
			<li>Spring Cloud Eureka</li>
			<li>Spring Cloud Config</li>
			<li>Spring Cloud Zuul</li>
			<li>Spring Cloud Security</li>
			<li>Spring Cloud OpenFeign</li>
			<li>Spring Cloud Hystrix</li>
		</ul>
	</li>
	<li>Mongo</li>
	<li>apache.poi</li>
	<li>Bootstrap3, Echarts, JavaScript, Ajax, HTML</li>
</ul>
