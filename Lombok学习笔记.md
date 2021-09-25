## Lombok的学习

### @slf4j中log.info()的作用

在@slf4j下我们有一个非常好用的方法，它是log.info()

它可以从前端获取参数，这样它的应用将会非常广泛，例如我们可以利用它来获取输入的账号密码，用户的个人信息，或者输入的信息等。

**使用方法：**

一下是一段如何使用log.info()的代码，它的功能是向数据库中插入我们输入的雇员信息，但是要记住一点一定要加@slf4j注解。

```java
    @GetMapping("InsertEMP")
    public String InsertEMP(Integer id,String firstname, String lastname,String email){
        log.info("id:{}",id);
        log.info("firstname:{}",firstname);
        log.info("lastname:{}",lastname);
        log.info("email:{}",email);
        Employees emp=new Employees();
        emp.setId(id);
        emp.setFirstName(firstname);
        emp.setLastName(lastname);
        emp.setEmail(email);
        employeesService.insert(emp);
        return "InsertSuccess";
    }
```

我们如何输入？方法如下所示

```url
http://localhost:8080/employees/InsertEMP?id=8&firstname=这是来自Spring输入的test&lastname=胡桃夹子&email=野蜂飞舞
```

这样我们就可以输入我们需要的信息。

### @Autowired或者@Resource的用法和作用


这个注解就是spring可以自动帮你把bean里面引用的对象的setter/getter方法省略，它会自动帮你set/get。

<bean id="userDao" class="..."/>

<bean id="userService" class="...">

    <property name="userDao">
    
      <ref bean="userDao"/>
    
    </property>

</bean>

这样你在userService里面要做一个userDao的setter/getter方法。

但如果你用了@Autowired的话，你只需要在UserService的实现类中声明即可。

**使用了@AutoWired或者@Resource后我们就可以调用Service层的服务了**

**例子:**

```java
    @Resource
    private EmployeesService employeesService;
```

或者

```java
    @Autowired
    EmployeesService employeesService;
```

两者功能类似，这里就不深究其区别了
