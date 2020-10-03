# Investment management system

This is a investment management system. User can use this system to manage data about income, expenses and investment portfolios. And this systemcan provide a real time cost analysis information and a highly filterable activity dashboard to keep track of users account activity such as deposits, withdrawals and executed trades.

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
