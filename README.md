# api_gateway

Репозиторий содержит в себе EurekaServer и минимально настроенный API Gateway на базе Spring Cloud, подключенный к Keycloak для авторизации пользователей.

**Для начала работы необходимо:**

Клонировать репозиторий

```angular2html
git clone https://github.com/NikKha03/api_gateway.git
```

Добавить ```application.yaml``` файл

```angular2html
cd api_gateway/ApiGateway/src/main/resources && touch application.yaml
```

Заполнить ```application.yaml``` файл своими данными

```angular2html
eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/  
    register-with-eureka: true   
    fetch-registry: true         
  instance:
    prefer-ip-address: true
server:
  port: 8080

dop-urls:
  main-page: your-url
  allowed-origins: your-origins

spring:
  main:
    web-application-type: reactive
  application:
    name: ApiGateway
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true
  security:
    oauth2:
      client:
        registration:
          keycloak:
            client-id: your-client-id
            client-secret: your-client-secret
            redirect-uri: your-redirect-uri
            scope:
              - openid
              - microprofile-jwt
            clientName: Keycloak
        provider:
          keycloak:
            issuer-uri: your-issuer-uri
            user-name-attribute: preferred_username
```
По _redirect-uri_ пользователь перенаправляется на страницу авторизации.

**После авторизации через API Gateway можно сделать с клиента GET запрос на получение данных авторизованного пользователя:**

```http://localhost:8761/apiEureka/user/get```
