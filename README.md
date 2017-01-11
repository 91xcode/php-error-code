# 使用

在ErrorCode里添加const，并且写上改code的注释，然后php执行：

```
   $jsonDoc = (new ErrorCode())->documentGenerate(true);
```

就会生成Error Code的文档了。

Error Code 一般都是从1000开始的，1000以内被Http协议占用。




