# Spring Cloud Netflix
Spring Cloud Netflix は順次メンテナンスモードへ移行中

### 参考
 - [what happens in spring cloud netflix](https://www.slideshare.net/apkiban/what-happens-in-spring-cloud-netflix)
 - [Modules In Maintenance Mode](https://cloud.spring.io/spring-cloud-netflix/multi/multi__modules_in_maintenance_mode.html)

## Spring Cloud Netflix Eureka
サービスディスカバリ。
Eureka は現時点ではメンテナンスモード対象ではないが、Spring Cloud Zookeeper への移行が検討されているという噂もある。

## Spring Cloud Netflix Ribbon
ロードバランサ。
Spring Cloud Netflix Ribbon はメンテナンスモードへ。
Spring Cloud Load Balancer への移行が推奨。

## Spring Cloud Netflix Zuul
APIゲートウェイ。
Spring Cloud Netflix Zuul はメンテナンスモードへ。
Spring Cloud Gateway への移行が推奨。

## Spring Cloud Netflix Hystrix
サーキットブレーカ。
Spring Cloud Netflix Hystrix はメンテナンスモードへ。
Spring Cloud Circuit Breaker + Resilience4J への移行が推奨。

