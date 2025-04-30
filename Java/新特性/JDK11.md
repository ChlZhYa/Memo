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
