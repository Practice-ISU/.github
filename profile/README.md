# Practice-ISU

![Flutter](https://img.shields.io/badge/Flutter-%2302569B.svg?style=for-the-badge&logo=Flutter&logoColor=white)
![C#](https://img.shields.io/badge/c%23-%23239120.svg?style=for-the-badge&logo=c-sharp&logoColor=white)
![Go](https://img.shields.io/badge/go-%2300ADD8.svg?style=for-the-badge&logo=go&logoColor=white)

![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white)
![Postgres](https://img.shields.io/badge/postgres-%23316192.svg?style=for-the-badge&logo=postgresql&logoColor=white)

![License MIT](https://img.shields.io/github/license/Ileriayo/markdown-badges?style=for-the-badge)

Practice-ISU is an organization that provides microservices for cloud file hosting. The application architecture consists of a client (Flutter) connected to an API gateway that serves as a bridge between microservices and the client. Currently, three microservices are available, including Discovery-service, User-service, and Storage-service.

## Architecture

![Architecture](https://github.com/Practice-ISU/.github/blob/main/images/pt.png)

The application represents a connection between the [client](https://github.com/Practice-ISU/web-client) (Flutter) and the [API gateway](https://github.com/Practice-ISU/gatekeeper), which is the link between the microservices and the client. Currently, three microservices have been implemented:

- Discovery-service
- User-service
- Storage-service

### [Discovery-service](https://github.com/Practice-ISU/discovery-service)

Discovery-service is a microservice that plays a key role in the overall application architecture. When a request comes from the client, the API gateway queries the discovery-service to determine whether the required microservices needed to fulfill the request are available or not.

Discovery-service combines two GRPC services to facilitate communication between microservices and the API gateway. These two services are:

1. Registration - This service is responsible for registering microservices in the repository and assigning channels for API-gateway to interact with specific microservices. The registration service is a crucial component of the discovery-service since it guarantees that only registered microservices are available for use.
2. Ping - After registering a microservice, the discovery-service sends pings to check the availability of the microservice. This service is an important component of the discovery-service since it ensures that only available microservices are used to fulfill requests.

### [User-service](https://github.com/Practice-ISU/user-service)

User-service is an important component of the internal microservice architecture of the Practice-ISU project. This microservice handles a wide range of user-related tasks, including registration, authentication, token verification, and user data retrieval. It is designed for access through a GRPC server, allowing for faster and more efficient communication between the user-service and other microservices.

As an internal microservice, user-service is registered in the discovery-service, which is a centralized registration and ping service for all microservices in the application. When a request comes from the client, the API gateway uses the discovery-service to determine whether the required microservices are available to fulfill the request. If the user-service is unavailable or not registered, the API gateway will not direct the request to that microservice. This ensures that only available and registered microservices are used to fulfill requests, thereby improving the overall performance of the application.

### [Storage-service](https://github.com/Practice-ISU/storage-service)

Storage-service is an internal microservice that functions as a file and folder management system. This service provides users with various functions, such as adding, deleting, and retrieving folder information, retrieving all folders for a specific user, as well as adding, deleting, and retrieving files in various formats, including static files, base64, and zip archives.

To access Storage-service, it is registered in the discovery-service, which is a centralized registration and ping service for all microservices in the application. This registration ensures that only available and registered microservices are used to fulfill requests, improving the overall performance of the application. In addition, the service closely collaborates with the discovery-service by providing its IP address, allowing other microservices to easily locate and communicate with it, further improving the efficiency of the application.
