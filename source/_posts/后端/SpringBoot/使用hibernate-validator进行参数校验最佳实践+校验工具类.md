---
title: 使用hibernate-validator进行参数校验最佳实践+校验工具类
date: 2021-07-15 10:23:37
permalink: /pages/a1b42c/
categories:
  - 后端
  - SpringBoot
tags:
  - 
---
在我们用Controller接收参数后，往往需要对参数进行校验。如果我们手写校验的话，就会有一堆的判空代码，看起来很不优雅，写起来也费时费力。下面来看下如何通过hibernate-validator来进行优雅的参数校验。

## 首先需要引入依赖：

```xml
<dependency>
	<groupId>org.hibernate.validator</groupId>
	<artifactId>hibernate-validator</artifactId>
	<version>6.2.0.Final</version>
</dependency>
```



## hibernate-validator注解

`hibernate-validator`提供了很多注解来让我们进行参数校验：

### 常用的校验注解如下表所示：

| 注解               | 说明                                                         |
| ------------------ | ------------------------------------------------------------ |
| @NotNull           | 被注释的元素（任何元素）必须不为null，但集合为空也是可以的。对集合来说没啥实际意义 |
| @NotEmpty          | 用来校验字符串、集合、map、数组不能为null或空 （字符串传入空格也不可以）（集合需至少包含一个元素）功能强于@NotNull |
| @NotBlank          | 只用来校验字符串不为null，不为空值，不为全空格。功能强大于@NotEmpty |
| @Size(max=, min=)  | 指定的字符串、集合、map、数组长度必须在指定的max和min范围内。（允许元素为null，字符串允许为空格） |
| @Length(min=,max=) | 只用来校验字符串，长度必须在指定的max和min范围内。（允许元素为null） |
| @Range(min=,max=)  | 用来校验数字或字符串的大小必须在指定的min和max范围内，字符串会转成数字进行比较，如果不是数字校验不通过。（允许元素为null） |
| @Min()             | 校验数字（包括integer、short、long、int等）的最小值，不支持小数即double和float。（允许元素为null） |
| @Max()             | 校验数字（包括integer、short、long、int等）的最大值，不支持小数即double和float。（允许元素为null） |
| @Pattern()         | 正则表达式匹配，可用来校验年月日格式是否包含特殊字符         |

### @Valid	

递归的对关联对象进行校验，如果关联对象是个集合或者数组，那么对其中的元素进行递归校验，如果是一个map，则对其中的值部分进行校验
主要区分下@NotNull、@NotEmpty、@NotBlank 3个注解的区别：
（1）@NotNull：任何对象的value不能为null。
（2）@NotEmpty：集合对象的元素不为0，即集合不为空，也可以用于字符串不为null。
（3）@NotBlank：只能用于字符串不为null，并且字符串trim()以后length要大于0。

#### 需要注意如下几点：

（1）除了@Empty要求字符串不能全是空格，其他的字符串校验都是允许空格的。
（2）message是可以引用常量的，但是如@Size里max不允许引用对象常量，基本类型常量是可以的。message是错误提示信息，是可以返回给前台的。
（3）大部分规则校验都是允许参数为null，即当不存在这个值时，就不进行校验了。

### 不太常用的校验注解如下表所示：

| 注解                          | 说明                                                     |
| ----------------------------- | -------------------------------------------------------- |
| @Null                         | 被注释的元素必须为null                                   |
| @AssertTrue                   | 被注释的元素必须为true                                   |
| @AssertFalse                  | 被注释的元素必须为false                                  |
| @DecimalMin(value=，message=) | 被注释的元素必须是一个数字，其值必须大于等于指定的最小值 |
| @DecimalMax(value=,message=)  | 被注释的元素必须是一个数字，其值必须小于等于指定的最大值 |
| @Digits (integer, fraction)   | 被注释的元素必须是一个数字，其值必须在可接受的范围内     |
| @Past                         | 被注释的元素必须是一个过去的日期                         |
| @Future                       | 被注释的元素必须是一个将来的日期                         |
| @Email                        | 被注释的元素必须是电子邮箱地址                           |

## 代码实战

### 1.使用BindingResult获取检验结果

我们可以使用`BindingResult`获取检验结果，构造友好的返回信息

Controller中的代码如下：

```java
@Api(tags = "校验框架")
@RestController
@RequestMapping("/validate")
public class ValidatedController {
 
 
    @ApiOperation(value = "bindValidate")
    @PostMapping("bindValidate")
    public ValidatedVO bindValidate(@RequestBody @Validated(value= {ValidatedGroup.DELET.class}) ValidatedVO validatedVO, BindingResult result) {
        if (result.hasErrors()) {
            StringBuilder message = new StringBuilder("参数校验失败：");
            List<ObjectError> errors = result.getAllErrors();
            for (ObjectError error : errors) {
                message.append(error.getDefaultMessage()).append(".");
            }
            throw HttpError.error(111, message.toString());
        }
        return validatedVO;
    }
 
 
}
```

我们用以下实体类来作为Controller的参数接收实体

```java
import lombok.Data;
 
import javax.validation.constraints.NotBlank;
import javax.validation.constraints.NotNull;
 
@Data
public class ValidatedVO {
 
    //更新、删除时不能为空
    @NotNull(message = "id不能为空", groups = {ValidatedGroup.UPDATE.class, ValidatedGroup.DELET.class})
    private Long id;
 
    //新增、更新时不能为空
    @NotBlank(message = "name不能为空", groups = {ValidatedGroup.CREATE.class ,ValidatedGroup.UPDATE.class})
    private String name;
 
    //查询时不能为空
    @NotBlank(message = "queryParam不能为空", groups = {ValidatedGroup.QUERY.class})
    private String queryParam;
 
}
```



分组的类：

```java
public class ValidatedGroup {
 
    public interface CREATE{}
 
    public interface DELET{}
 
    public interface UPDATE{}
 
    public interface QUERY{}
}
```


需要注意的是，@Validated支持分组校验，即校验注解中的groups属性。这个为我们的校验也提供了便利。我们可以在Controller需要校验的参数前用@Validated的value属性来表示需要校验的分组，那么就会只会校验实体对象中拥有相同的分组的属性。这样我们就可以只用一个实体满足不同的场景了。

启动项目后,我们在swagger上请求，传递空的json字符串【{}】，返回结果：

```json
{
  "code": 111,
  "message": "参数校验失败：id不能为空."
}
```

 然而每次都需要在请求进来时用BindingResult做处理，很不优雅。

### 2.通过@RestControllerAdvice统一处理参数校验信息

如果我们不用BindingResult获取校验结果，即不做处理，框架就会抛出异常，响应400码，返回一些不友好的错误信息。即用如下代码：

```java
@ApiOperation(value = "bindValidate")
    @PostMapping("bindValidate")
    public ValidatedVO bindValidate(@RequestBody @Validated(value= {ValidatedGroup.DELET.class}) ValidatedVO validatedVO/*, BindingResult result*/) {
        /*if (result.hasErrors()) {
            StringBuilder message = new StringBuilder("参数校验失败：");
            List<ObjectError> errors = result.getAllErrors();
            for (ObjectError error : errors) {
                message.append(error.getDefaultMessage()).append(".");
            }
            throw HttpError.error(111, message.toString());
        }*/
        return validatedVO;
    }
```




那么我们可以使用@RestControllerAdvice来对异常进行处理，进行友好信息的提示

如果对@RestControllerAdvice和@ControllerAdvice不了解的，可以去查询学习，这里不进行讲述

```java
@RestControllerAdvice
public class GlobalExceptionHandler {    
 
    @ExceptionHandler(Exception.class)
    public CommonErrorVO handle(Exception e){
        if (e instanceof HttpError) {
            HttpError error = (HttpError)e;
            return CommonErrorVO.builder().code(error.getCode()).message(error.getMessage()).build();
        } else if (e instanceof MethodArgumentNotValidException) {
            MethodArgumentNotValidException validException = (MethodArgumentNotValidException) e;
            StringBuilder message = new StringBuilder("");
            validException.getBindingResult().getAllErrors().forEach(err -> {
                message.append(err.getDefaultMessage()).append(".");
            });
            return CommonErrorVO.builder().code(888).message(message.toString()).build();
        } else {
            return CommonErrorVO.builder().code(999).message(e.getMessage()).build();
        }
    }    
} 
```

MethodArgumentNotValidException异常即为hibernate-validator校验不通过抛出的异常信息，我们从其中获取到校验失败的信息来进行组装。

如上，我们通过@Validated配合@RestControllerAdvice完成了优雅的参数校验。

为了体现分组校验的便利性，我做了如下的测试，如果每个请求参数都是空的json字符串【{}】的话,那么它会根据指定的group来只校验带有相应group的属性。代码以及返回结果如下：

```java
@Api(tags = "校验框架")
@RestController
@RequestMapping("/validate")
public class ValidatedController {
 
    /**
     * @Validated注解表示开启Spring的校验机制，支持分组校验,声明在入参上。
     * @param validatedVO
     * @return
     */
    @ApiOperation(value = "分组校验:QUERY参数校验")//返回 【queryParam不能为空】
    @PostMapping("queryValidate")
    public ValidatedVO queryValidate(@RequestBody @Validated(value= {ValidatedGroup.QUERY.class}) ValidatedVO validatedVO) {
        return validatedVO;
    }
 
    @ApiOperation(value = "分组校验:CREATE参数校验")// 返回 【name不能为空】
    @PostMapping("createValidate")
    public ValidatedVO createValidate(@RequestBody @Validated(value= {ValidatedGroup.CREATE.class}) ValidatedVO validatedVO) {
        return validatedVO;
    }
 
    @ApiOperation(value = "分组校验:UPDATE参数校验") // 返回【id不能为空.name不能为空.】
    @PostMapping("updateValidate")
    public ValidatedVO updateValidate(@RequestBody @Validated(value= {ValidatedGroup.UPDATE.class}) ValidatedVO validatedVO) {
        return validatedVO;
    }
 
    @ApiOperation(value = "分组校验:DELETE参数校验") //返回 【id不能为空】
    @PostMapping("deleteValidate")
    public ValidatedVO deleteValidate(@RequestBody @Validated(value= {ValidatedGroup.DELET.class}) ValidatedVO validatedVO) {
        return validatedVO;
    }
}
```

以上的内容我们讲的都是带有group的校验，那么如果我们的参数只在单一场景使用，即只在一个接口上使用，那么校验的类的属性上无需设置groups，Controller上@Validated注解也无需用value属性指定group。如果校验的类上设置了groups，@Validated注解却未指定group，那么校验是不生效的。

### 单一场景的校验代码如下：

```java
@ApiOperation(value = "noGroupValidate参数校验")
@PostMapping("noGroupValidate")
public NoGroupValidatedVO noGroupValidate(@RequestBody @Validated NoGroupValidatedVO noGroupValidatedVO) {
    return noGroupValidatedVO;
}
```



```java
@Data
public class NoGroupValidatedVO {
 
    @NotNull(message = "id不能为空")
    private Long id;
 
    @NotBlank(message = "name不能为空")
    private String name;
 
    @NotBlank(message = "queryParam不能为空")
    private String queryParam;
 
}
```



### 非Controller中的校验

以上内容中我们讲解的都是在Controller方法上的参数校验，那如果要在其他的类（在Spring管理下）的方法上做参数校验，该如何使用呢？

```java
@Service
@Validated(value= {ValidatedGroup.DELET.class})
public class ValidateService {
 
    public ValidatedVO innerValidate(@Valid ValidatedVO validatedVO) {
        return validatedVO;
    }
}
```

如上，我们需要在类上使用@Validated注解，在方法上使用@Valid注解。但是，由于用在类上@Validated可以指定group，而@Valid不能指定，这就导致这种方式使用起来有局限性。

建议使用如下工具类进行校验。

## 校验工具类



```java
@Api(tags = "校验框架")
@RestController
@RequestMapping("/validate")
public class ValidatedController {
 
    /**
     * @Validated注解表示开启Spring的校验机制，支持分组校验,声明在入参上。
     * @param validatedVO
     * @return
     */
    @ApiOperation(value = "分组校验:QUERY参数校验")//返回 【queryParam不能为空】
    @PostMapping("queryValidate")
    public ValidatedVO queryValidate(@RequestBody @Validated(value= {ValidatedGroup.QUERY.class}) ValidatedVO validatedVO) {
        return validatedVO;
    }
 
    @ApiOperation(value = "分组校验:CREATE参数校验")// 返回 【name不能为空】
    @PostMapping("createValidate")
    public ValidatedVO createValidate(@RequestBody @Validated(value= {ValidatedGroup.CREATE.class}) ValidatedVO validatedVO) {
        return validatedVO;
    }
 
    @ApiOperation(value = "分组校验:UPDATE参数校验") // 返回【id不能为空.name不能为空.】
    @PostMapping("updateValidate")
    public ValidatedVO updateValidate(@RequestBody @Validated(value= {ValidatedGroup.UPDATE.class}) ValidatedVO validatedVO) {
        return validatedVO;
    }
 
    @ApiOperation(value = "分组校验:DELETE参数校验") //返回 【id不能为空】
    @PostMapping("deleteValidate")
    public ValidatedVO deleteValidate(@RequestBody @Validated(value= {ValidatedGroup.DELET.class}) ValidatedVO validatedVO) {
        return validatedVO;
    }
}
```

使用起来很简单，只需要将带有属性校验注解的类的对象传入即可：

```java
NoGroupValidatedVO noGroupValidatedVO = new NoGroupValidatedVO();
String check1 = ValidateUtil.validateParams(noGroupValidatedVO);//不生效
ValidatedVO validatedVO = new ValidatedVO();
String check2 = ValidateUtil.validateParams(validatedVO, ValidatedGroup.CREATE.class);
```

### 嵌套校验

前面的内容的校验都是单个对象的校验，那么如果嵌套对象怎么校验呢？

使用嵌套校验的话，Controller方法上的参数注解，或者非Controller上的参数注解，又或者是使用校验工具类，用法都是一样的。不一样的是需要校验的实体需要改进下。以Controller上校验为例：

```java
@ApiOperation(value = "嵌套校验: nestedValidate校验")
@PostMapping("nestedValidate")
public ParentVO nestedValidate(@RequestBody @Validated(value = {ValidatedGroup.UPDATE.class}) ParentVO parentVO) {
    return parentVO;
}
```

ParentVO如下：

```java
@Data
public class ParentVO {
    @NotBlank(message = "parentName不能为空", groups = {ValidatedGroup.UPDATE.class})
    private String parentName;

    @Valid
    @NotNull(message = "child不能为空", groups = {ValidatedGroup.UPDATE.class})
    private ChildVO child;

    @Data
    public static class ChildVO {

        @NotBlank(message = "childName不能为空", groups = {ValidatedGroup.UPDATE.class})
        private String childName;
    }
}
```


只需要在嵌套的对象上加@Valid注解即可。
————————————————
版权声明：本文为CSDN博主「kusedexingfu」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/kusedexingfu/article/details/116676271