---
layout: post
title: "Getting Started with Spring Boot’s WebClient"
description: "An introduction to using Spring Boot’s WebClient—the modern, reactive replacement for RestTemplate."
date: 2025-09-01 10:00:00 +0530
categories: [SPRING, WEBCLIENT]
tags: [PROGRAMMING]
media_subpath: /assets/img/2025-09-01-getting-cozy-with-spring-boot-s-webclient
image:
    path: /webclient-header.png
    alt: Header image
    height: 50 px
---

**WebClient** is Spring’s modern, reactive HTTP client. It was introduced in **Spring 5** as part of the *WebFlux* module and is considered the successor to *RestTemplate*. WebClient is non-blocking and supports both reactive and traditional applications.

---

## Why WebClient?

* Provides a **reactive, non-blocking API**.
* Can still be used in traditional Spring MVC applications.
* Designed to be more flexible and powerful compared to `RestTemplate`.

---

## Adding the Dependency

To use WebClient, include the WebFlux starter in your project:

**Maven**

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-webflux</artifactId>
</dependency>
```

**Gradle**

```groovy
implementation 'org.springframework.boot:spring-boot-starter-webflux'
```

---

## Creating a WebClient

You can create a WebClient in different ways:

1. **Default instance:**

   ```java
   WebClient client = WebClient.create();
   ```

2. **With a base URL:**

   ```java
   WebClient client = WebClient.create("http://localhost:8080");
   ```

3. **Using builder with custom configuration:**

   ```java
   WebClient client = WebClient.builder()
       .baseUrl("https://api.example.com")
       .defaultHeader(HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_JSON_VALUE)
       .defaultCookie("sessionId", "abc123")
       .build();
   ```

---

## Making Requests

Example of using WebClient in a Spring service:

```java
@Service
public class MyService {

    private final WebClient webClient;

    public MyService(WebClient.Builder webClientBuilder) {
        this.webClient = webClientBuilder
            .baseUrl("http://example.org")
            .build();
    }

    public Mono<Details> getDetails(String name) {
        return webClient.get()
            .uri("/{name}/details", name)
            .retrieve()
            .bodyToMono(Details.class);
    }
}
```

`.retrieve()` is recommended over the older `.exchange()` method.

---

## Working with Parameters and URIs

You can add query parameters and dynamic paths using `uriBuilder`:

```java
webClient.get()
  .uri(uriBuilder -> uriBuilder
      .path("/products/{id}")
      .queryParam("category", "widgets")
      .queryParam("tags", "blue", "large")
      .build(productId))
  .retrieve()
  .bodyToMono(Product.class)
  .block(); // use with caution in reactive flows
```

---

## Logging Requests and Responses

### Option 1: Using Filters

```java
WebClient.builder()
  .filter(logRequest())
  .filter(logResponse())
  .build();
```

```java
private ExchangeFilterFunction logRequest() {
    return ExchangeFilterFunction.ofRequestProcessor(req -> {
        log.info("Request: {} {}", req.method(), req.url());
        req.headers().forEach((n, v) -> v.forEach(val -> log.info("{}={}", n, val)));
        return Mono.just(req);
    });
}

private ExchangeFilterFunction logResponse() {
    return ExchangeFilterFunction.ofResponseProcessor(res -> {
        log.info("Response status: {}", res.statusCode());
        res.headers().asHttpHeaders().forEach((n, v) -> v.forEach(val -> log.info("{}={}", n, val)));
        return Mono.just(res);
    });
}
```

### Option 2: Netty Wiretap

When you use **Spring WebFlux** with `spring-boot-starter-webflux`, it runs on top of **Reactor Netty**.
The **Wiretap** feature in Netty is essentially a **logging mechanism** that lets you see detailed information about HTTP requests and responses.

Think of it as a transparent “tap” into the network traffic.

With Wiretap enabled, you can see:

* HTTP methods and URLs (e.g., `GET /products/1`)
* Request and response headers
* Request and response bodies (if text-based and small enough)
* TCP connection events (connect, disconnect)

---

## How to Enable Wiretap in Spring WebClient

To enable Wiretap, configure the `ReactorClientHttpConnector` with a `HttpClient` that has wiretap enabled:

```java
import org.springframework.web.reactive.function.client.WebClient;
import reactor.netty.http.client.HttpClient;
import org.springframework.http.client.reactive.ReactorClientHttpConnector;

WebClient webClient = WebClient.builder()
    .clientConnector(new ReactorClientHttpConnector(
        HttpClient.create().wiretap(true)
    ))
    .build();
```

---

## What You’ll See in Logs

When enabled, Wiretap prints logs at the `DEBUG` level. Example:

```
[reactor.netty.http.client.HttpClient] [id: 0x1a2b3c4d] REGISTERED
[reactor.netty.http.client.HttpClient] [id: 0x1a2b3c4d] CONNECT: localhost/127.0.0.1:8080
[reactor.netty.http.client.HttpClient] [id: 0x1a2b3c4d] WRITE: 123B GET /api/data HTTP/1.1
[reactor.netty.http.client.HttpClient] [id: 0x1a2b3c4d] READ: 456B HTTP/1.1 200 OK
```

Depending on configuration, request and response payloads may also be shown.

---

## Configuring Logging Verbosity

Wiretap relies on your logging configuration. By default, Spring Boot uses `INFO` level, so you won’t see Wiretap logs.

To view them, enable `DEBUG` for Reactor Netty in `application.yml`:

```yaml
logging:
  level:
    reactor.netty: DEBUG
    reactor.netty.http.client: DEBUG
```

---

## When Should You Use Netty Wiretap?

* During **development** to understand how WebClient sends/receives requests
* For **debugging integration issues** with APIs
* For **performance troubleshooting**, to see connection lifecycle events

---

## Conclusion

WebClient is the modern alternative to RestTemplate, offering non-blocking, reactive capabilities while remaining flexible enough for traditional applications. It is a recommended choice for new Spring projects.

---
