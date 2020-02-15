# @RestController
```md
@RestController注解相当于@ResponseBody ＋ @Controller合在一起的作用
```

## vs. @Controller
```md
1. 如果只是使用@RestController注解Controller，则Controller中的方法无法返回jsp页面，或者html，
    配置的视图解析器 InternalResourceViewResolver不起作用，返回的内容就是Return 里的内容。
2. 如果需要返回到指定页面，则需要用 @Controller配合视图解析器InternalResourceViewResolver才行。
    如果需要返回JSON，XML或自定义mediaType内容到页面，则需要在对应的方法上加上@ResponseBody注解。
```