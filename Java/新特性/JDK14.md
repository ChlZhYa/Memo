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
