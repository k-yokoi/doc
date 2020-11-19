# Spring Cloud Netflix Eureka
サービスディスカバリ。
Eureka サーバーと Eureka クライアントの2つの設定が必要。

## 参考
- [サービス登録およびディスカバリ](https://spring.pleiades.io/guides/gs/service-registration-and-discovery/)
- [Spring I/O 2018 報告会 - Spring Cloud Gateway / Spring Cloud Pipelines ](https://www.slideshare.net/JunyaKatada/spring-io-2018-spring-cloud-gateway-spring-cloud-pipelines)

## Eureka サーバー
### 依存関係に追加
依存関係を`pom.xml`に追加。
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

### @EnableEurekaServer の追加
Eureka サービスレジストリ を起動するために、@EnableEurekaServer の追加。
```
package com.example.serviceregistrationanddiscoveryservice;

......

@EnableEurekaServer
@SpringBootApplication
public class ServiceRegistrationAndDiscoveryServiceApplication {

	public static void main(String[] args) {
		SpringApplication.run(ServiceRegistrationAndDiscoveryServiceApplication.class, args);
	}
}
```

### アプリケーションプロパティの設定
テスト目的の設定を記述。
下記の記述では本番環境に適さない点に注意。
```
server.port=8761

eureka.client.register-with-eureka=false
eureka.client.fetch-registry=false

logging.level.com.netflix.eureka=OFF
logging.level.com.netflix.discovery=OFF
```

### 起動
`mvn spring-boot:run`

## Eureka クライアント
## 依存関係に追加
依存関係を`pom.xml`に追加。
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
```

### @EnableDiscoveryClient の追加
```
package com.example.serviceregistrationanddiscoveryclient;

......

@EnableDiscoveryClient
@SpringBootApplication
public class ServiceRegistrationAndDiscoveryClientApplication {

	public static void main(String[] args) {
		SpringApplication.run(ServiceRegistrationAndDiscoveryClientApplication.class, args);
	}
}
```