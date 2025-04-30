## 字符串方法
为字符串添加了新的基础方法，例如：`isBlank`、`lines`、`strip`等。用于来简化代码中对于字符串的处理。
在实际项目开发中，通常使用 apache-commons 来处理字符串，这些改动意义不大。

## 本地变量

```Java
List<String> sampleList = Arrays.asList("Java", "Kotlin");
String resultString = sampleList.stream()
  .map((@Nonnull var x) -> x.toUpperCase())
  .collect(Collectors.joining(", "));
assertThat(resultString).isEqualTo("JAVA, KOTLIN");
```
通过 var 关键字来接收返回对象，可以省略掉一些中间处理对象的类型定义。

## HTTP 客户端
```Java
HttpClient httpClient = HttpClient.newBuilder()
  .version(HttpClient.Version.HTTP_2)
  .connectTimeout(Duration.ofSeconds(20))
  .build();
HttpRequest httpRequest = HttpRequest.newBuilder()
  .GET()
  .uri(URI.create("http://localhost:" + port))
  .build();
HttpResponse httpResponse = httpClient.send(httpRequest, HttpResponse.BodyHandlers.ofString());
assertThat(httpResponse.body()).isEqualTo("Hello from the server!");
```
Java11 中原生HTTP工具类增加了对 HTTP2版本的支持，在生产项目中，一般会通过第三方工具类来实现 HTTP 访问，意义不大。