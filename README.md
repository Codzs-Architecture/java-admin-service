# Spring Boot Admin Server Repository

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) ![GitHub issues](https://img.shields.io/github/issues/khaitan-nitin/java-admin-service)


Welcome to the Admin Server Repository! This repository contains the source code for a admin server written in Spring Boot and Java that uses Spring Boot Admin dependency. This Admin Server is designed to centralize and manage application's/microservice's logs, CPU, Memory, JVM, configuration & monitoring, making it easy to maintain multiple services.

## Table of Contents
* [Getting Started](#getting-started)
    * [Prerequisites](#prerequisites)
    * [Setup](#setup)
* [Usage](#usage)
* [Swagger](#swagger)
* [Configuration](#configuration)
* [Contributing](#contributing)
* [License](#license)

## Getting Started
Follow these instructions to get the Admin Server up and running in your local development environment.

### Prerequisites
Make sure you have the following installed:

* Java Development Kit (JDK) 17 or later
* Maven
* Git

### Setup
1.  Copy all the 3 repositories to your local machine in the same folder.
2.  Clone the `sample config repository` to your local machine:
    ```
    git clone https://github.com/khaitan-nitin/java-codzs-config.git
    cd java-codzs-config
    ```
3.  Clone the `sample keys repository` to your local machine:
    ```
    git clone https://github.com/khaitan-nitin/java-codzs-resource.git
    cd java-codzs-resource
    ```
4.  Clone the `admin server repository` to your local machine:
    ```
    git clone https://github.com/khaitan-nitin/java-admin-service.git
    cd java-admin-service
    ```
5.  Build the `admin server project` using Maven:
    ```
    mvn clean install
    ```
6.  Run the Config Server:
    ```
    java -Dspring.profiles.active=local -Dconfig.password=password -Dconfig.server.url=https://local.codzs.com:5002 -Dserver.ssl.key-store=./../java-codzs-resource/local/local.codzs.com.p12 -Dserver.ssl.key-store-password=localpassword -Dserver.ssl.key-password=localpassword -Djavax.net.ssl.trustStore=/Users/nitinkhaitan/Nitin/Code/codzs/java/java-microserivce-project/java-codzs-resource/local/local.codzs.com.truststore.p12 -Djavax.net.ssl.trustStorePassword=localpassword -Djavax.net.ssl.trustStoreType=PKCS12 -Dadmin.password=admin123 -jar target/java-admin-service.jar
    ```
    * `spring.profiles.active`: current active profile as per the environment
    * `config.server.url`: Config server base URL
    * `config.password`: Config server password
    * `server.ssl.key-store`: Path to the ssl key store file
    * `server.ssl.key-store-password`: SSL Key store password
    * `server.ssl.key-password`: SSL Key password
    * `admin.password`: Admin password

    To configure IDE, do the below entry in the environment variable in the IDE (and change the values as per your environment):
    ```
    -Dspring.profiles.active=local
    
    config.password=password; config.server.url=https://local.codzs.com:5002; server.ssl.key-store=./../java-codzs-resource/local/local.codzs.com.p12; server.ssl.key-store-password=localpassword; server.ssl.key-password=localpassword; admin.password=admin123
    ```

## Usage
To use the Admin Server in your Spring Boot application, you need to configure your application to connect to this server.

1.  In your Spring Boot application (i.e. - [`Resource Server`](https://github.com/khaitan-nitin/java-resource-service.git)), add the following dependency to your pom.xml:
    xml
    ```
    <!-- Add Spring Admin Client -->
    <dependency>
        <groupId>com.codzs</groupId>
        <artifactId>admin-client-service</artifactId>
    </dependency>
    ```
2.  In the resource service application's `bootstrap.yml` or `bootstrap.properties` or `application.yml`, we can configure the Admin server's client details as done in  [`sample config repository`](https://github.com/khaitan-nitin/java-codzs-config.git). The client detail are:
    ```
    spring:
        boot:
            admin:
                client:
                    url: https://local.codzs.com:5001
                    username: admin-service-user
                    password: '{cipher}AYAfdzcrkjwM4rt2jhkxezO5zBNmfljIeeBFXKsUMV8Q9ASYjBCv2lBtu2L7Se7hEK7DTDc1JxTmkiZW6dn14UhEdbpcSObqknAxiaK7wMBz3e6POdTZeIF1J/kCwBSvccEUGZuog1eZjQav14uE5wYQqyDfqnOPvak4JndzykJBjZ4SSzZNwOUYxQyRaA0gQbgYF+E+ZnY7BpwzfcT2DTpaZDPAYUBLFiCiY6bNbLBC3LS3i/Qq0/cv6OOz1Wl6ruwTQBrIHyrUiHOnbuj7MvBtl+VvaMyFaIFuxTDXZ7YxuxR4+l2Nd3eCqD2VDD63OrMlBWkcdBSJXOttIecqc+plciKAGdd4B8NIE/aD2oYChXKU/HDOyj6AoxJSSCjhGOBsa7T0j0w4ecqBwXNx8T9rp6fLpZxVWMZsJ53wcg2DfkbZSU2ZPeqYoCijK604HOVPDU8CcS1Rskj0wXrllvQRfXk0gt5PaVdlPCfKfMMX1fZKeglXtkYxMb5heyvpZsgy3Kl5VPXhjAcCatdKNrA/mMUwL8Bv2toFaBENp1nqIg=='
                    instance:
                        metadata:
                            user:
                                name: ${spring.security.user.name}
                                password: ${spring.security.user.password}
    ```
    Feel free to customise the client details as per your requirement.


## Swagger
Swagger is a set of open-source tools built around the OpenAPI Specification that can help you design, build, document and consume REST APIs. The url for the swagger is: https://local.codzs.com:5001/management/swagger-ui/index.html

## Configuration
The Config Server can be customized to suit various requirements. You can modify the following files and settings:

* `application.yml`: Basic Admin Server settings.
* `application-config-service.yml`: Config service connection details, to pull authorization server configuration details on startup.
* `application-keystore.yml`: Configuration for SSL settings.

For more advanced customization and features, refer to the Spring Cloud Config documentation.

## Contributing
We welcome contributions from the community! If you want to contribute to this project, please follow these steps:

* Fork the repository.
* Create a new branch for your changes.
* Make your changes and commit them with descriptive commit messages.
* Push your changes to your forked repository.
* Create a pull request, detailing the changes you made.

We appreciate your contributions, whether it's bug fixes, new features, or documentation improvements.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

