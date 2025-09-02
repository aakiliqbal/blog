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

**WebClient** is Spring’s modern, reactive HTTP client. Introduced in **Spring 5** as part of *WebFlux*, it is the successor to `RestTemplate`.  
Unlike `RestTemplate`, WebClient is **non-blocking** and works seamlessly in both reactive and traditional applications.

---

## Why WebClient?

* **Reactive, non-blocking API**
* Can be used in both **Spring MVC** and **Spring WebFlux**
* More **flexible and powerful** than `RestTemplate`

---

## Adding the Dependency

Add the WebFlux starter to your project:

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

You can create WebClient in multiple ways:

1. **Default instance:**

   ```java
   WebClient client = WebClient.create();
   ```

2. **With base URL:**

   ```java
   WebClient client = WebClient.create("http://localhost:8080");
   ```

3. **Custom builder:**

   ```java
   WebClient client = WebClient.builder()
       .baseUrl("https://api.example.com")
       .defaultHeader(HttpHeaders.CONTENT_TYPE, MediaType.APPLICATION_JSON_VALUE)
       .defaultCookie("sessionId", "abc123")
       .build();
   ```

---

## Making Requests

### GET Example

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

`.retrieve()` is preferred over the older `.exchange()`.

### POST Example (With Body)

```java
Mono<UserResponse> response = webClient.post()
    .uri("/users")
    .contentType(MediaType.APPLICATION_JSON)
    .bodyValue(new UserRequest("John", "Doe"))
    .retrieve()
    .bodyToMono(UserResponse.class);
```

### PUT Example (With Body)

```java
Mono<Product> updated = webClient.put()
    .uri("/products/{id}", 42)
    .contentType(MediaType.APPLICATION_JSON)
    .bodyValue(new Product("Laptop", 799.99))
    .retrieve()
    .bodyToMono(Product.class);
```

---

## Working with Parameters and URIs

```java
webClient.get()
  .uri(uriBuilder -> uriBuilder
      .path("/products/{id}")
      .queryParam("category", "widgets")
      .queryParam("tags", "blue", "large")
      .build(productId))
  .retrieve()
  .bodyToMono(Product.class)
  .block(); // avoid blocking in reactive flows
```

---

## Error Handling

WebClient provides flexible error handling. Instead of always relying on `.retrieve()`, you can use `.exchangeToMono()` to handle different status codes explicitly:

```java
Mono<String> response = webClient.get()
    .uri("/api/data")
    .exchangeToMono(res -> {
        if (res.statusCode().equals(HttpStatus.OK)) {
            return res.bodyToMono(String.class);
        } else if (res.statusCode().is4xxClientError()) {
            return Mono.just("Client error occurred");
        } else {
            return res.createException()
                .flatMap(Mono::error);
        }
    });
```

This approach allows you to:

* Return different results depending on status code  
* Gracefully handle `4xx` errors  
* Convert other errors into exceptions with `createException()`

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

With `spring-boot-starter-webflux`, WebClient runs on **Reactor Netty**.  
Netty’s **Wiretap** logs detailed request/response information including **headers and bodies** (for text-based payloads).

---

## Enabling Wiretap

```java
import org.springframework.web.reactive.function.client.WebClient;
import reactor.netty.http.client.HttpClient;
import org.springframework.http.client.reactive.ReactorClientHttpConnector;

WebClient webClient = WebClient.builder()
    .clientConnector(new ReactorClientHttpConnector(
        HttpClient.create()
            .wiretap("reactor.netty.http.client.HttpClient",
                LogLevel.DEBUG, AdvancedByteBufFormat.TEXTUAL)
    ))
    .build();
```

---

## Log Output Example

```
[reactor.netty.http.client.HttpClient] [id: 0x1a2b3c4d] REGISTERED
[reactor.netty.http.client.HttpClient] [id: 0x1a2b3c4d] CONNECT: localhost/127.0.0.1:8080
[reactor.netty.http.client.HttpClient] [id: 0x1a2b3c4d] WRITE: 123B POST /users HTTP/1.1
[reactor.netty.http.client.HttpClient] CONTENT: {"firstName":"John","lastName":"Doe"}
[reactor.netty.http.client.HttpClient] [id: 0x1a2b3c4d] READ: 456B HTTP/1.1 200 OK
[reactor.netty.http.client.HttpClient] CONTENT: {"id":1,"firstName":"John","lastName":"Doe"}
```

---

## Configuring Logging Verbosity

Enable DEBUG logs for Reactor Netty in `application.yml`:

```yaml
logging:
  level:
    reactor.netty: DEBUG
    reactor.netty.http.client: DEBUG
```

---

## When to Use Netty Wiretap?

* During **development** to inspect requests/responses  
* For **debugging API integration issues**  
* To analyze **connection lifecycle events**  

---

## Conclusion

WebClient is the modern alternative to RestTemplate, offering **non-blocking, reactive capabilities** while staying flexible for traditional applications.  
With built-in support for **custom error handling** and **detailed logging** (via filters or Wiretap), it is the recommended HTTP client for new Spring projects.

---
