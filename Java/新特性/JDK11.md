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

## Nest 访问控制
Java 11 扩展了对嵌套类的控制，对于嵌套类，可以实现内部类和外部类的互相访问，他们现在会编译在同一个嵌套类文件中。另外在 Java11 中通过反射可以实现内部类对外部类私有字段的访问，而在之前访问会抛出异常。

## Switch 表达式
JDK14 中，可以聚合同样操作的判断，而不是将每一个取值都作为一个分支。
```Java
boolean isTodayHoliday;
switch (day) {
    case "MONDAY":
    case "TUESDAY":
    case "WEDNESDAY":
    case "THURSDAY":
    case "FRIDAY":
        isTodayHoliday = false;
        break;
    case "SATURDAY":
    case "SUNDAY":
        isTodayHoliday = true;
        break;
    default:
        throw new IllegalArgumentException("What's a " + day);
}
```
在上面的判断中，周一到周五都是作为单独的分支进行判断。在 JDK14 中，可以聚合为一个分支：
```Java
boolean isTodayHoliday = switch (day) {
    case "MONDAY", "TUESDAY", "WEDNESDAY", "THURSDAY", "FRIDAY" -> false;
    case "SATURDAY", "SUNDAY" -> true;
    default -> throw new IllegalArgumentException("What's a " + day);
};
```

## 文本块
文本块的改动支持在代码中以可读的方式来拼接长文本。
例如：
```Java
String multiline = "A quick brown fox jumps over a lazy dog; the lazy dog howls loudly.";
```
可以通过 `\` 标记换行操作，按行来展示文本。
```Java
String multiline = """
    A quick brown fox jumps over a lazy dog; \
    the lazy dog howls loudly.""";
```
