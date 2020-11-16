# Spring Cloud Gateway
## 特徴
- Spring Framework、Spring Boot と組み合わせて使用
- 様々な要素でルーティングルールを設定
    - URLパス
    - ヘッダーやクッキーの値
    - メソッド（GET、POSTなど）
    - 時間（〇時以前、以降など）
- リクエスト、レスポンスの内容をフィルターで書き換え
- サーキットブレーカー、サービスディスカバリ、セキュリティの機能との統合も可能
- WebFluxを用いたノンブロッキング通信により、アクセス増加にも対応
- Netflix から Zuul という類似のライブラリがあるが、WebFlux を用いたときのSpringとの相性問題により、 Spring Cloud Gateway が推奨されてる

## 使い方
依存関係を追加する。
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```

`RouteLocator` Bean を作成する。
```
@Bean
public RouteLocator myRoutes(RouteLocatorBuilder builder) {
    return builder.routes().build();
}
```
全アクセスをルーティング。
```
builder.routes()
        .route("monolith", p -> p
                .path("/**")
                .uri("http://localhost:8081"))
        .build();
```
パスベースでルーティング
```
builder.routes()
        .route("hello", p -> p
                .path("/hello/**")
                .uri("http://localhost:8082"))
        .route("monolith", p -> p
                .path("/**")
                .uri("http://localhost:8081"))
        .build();
```
## サービスディスカバリとロードバランサを有効にする
依存関係を追加する。
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```
application.property に追記する。
```
spring.cloud.gateway.discovery.locator.enabled=true
```
内部でRibbonを使用しているため、下記を追記して `ReactiveLoadBalancerClientFilter` を代わりに使用するように設定する。
```
spring.cloud.loadbalancer.ribbon.enabled=false
```

Spring Cloud Gateway からサービスディスカバリを利用してアクセスするには、`lb://[hoge]`でアクセス。
これだけでロードバランサ機能も利用できる。
```
builder.routes()
        .route("hello", p -> p
                .path("/hello/**")
                .uri("lb://hello"))
```

## サーキットブレーカを有効にする
依存関係を追加する。
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-circuitbreaker-reactor-resilience4j</artifactId>
</dependency>
```
サーキットブレーカフィルターを追加して、有効にする。
```
    .route("hello", p -> p
            .path("/hello/**")
            .filters(f -> f
                    .circuitBreaker(c -> c
                            .setName("myCircuitBreaker")
                            .setFallbackUri("forward:/fallbackhello")))
            .uri("lb://hello"))
```