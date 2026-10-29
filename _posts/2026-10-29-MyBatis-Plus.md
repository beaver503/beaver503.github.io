---
title: MyBatis-Plus
date: 2026-10-29
categories: MyBatis-Plus
tags:
  - 博客
  - MyBatis-Plus
render_with_liquid: false
---
MyBatis-Plus 里面，一般是自己写一个 Service实现类，去继承 MP 自带的 `ServiceImpl` 这个类（不是MyBatis原生自带的，是MyBatis-Plus提供的）

### 1、标准写法（固定套路，企业后台开发标准写法）

MP给我们提供了一个通用实现类 `ServiceImpl<M extends BaseMapper<T>, T>`

- `M` = 你的Mapper接口
- `T` = 数据库对应的实体类

#### ① 第一步：Mapper接口（继承 BaseMapper）

```Java
// UserMapper.java
public interface UserMapper extends BaseMapper<User> {
}
```

#### ② 第二步：Service接口

```Java
public interface UserService extends IService<User> {
}
```

#### ③ 第三步：Service实现类，继承 `ServiceImpl`

```Java
// 两个泛型：第一个是Mapper，第二个是实体
@Service
public class UserServiceImpl extends ServiceImpl<UserMapper, User> implements UserService {
}
```

> `ServiceImpl` 就是MP提供好的通用实现，它已经帮你内置写好了： `save`、`getById`、`list`、`page分页`、`removeById`、updateById 这些基础CRUD，你不用自己写SQL。

### 2、关键点分清

1. `ServiceImpl`**不是MyBatis自带的！** 👉 它是 **MyBatis-Plus** 自己封装的工具类，MyBatis原生本身没有这个东西。 MyBatis原生只有Mapper接口，没有这种通用Service封装。
2. 泛型对应关系

```Java
// ServiceImpl<M, T>
// M：BaseMapper的实现类（Mapper接口）
// T：数据库实体
ServiceImpl<UserMapper, User>
```

- M = UserMapper
- T = User（实体）

3. 好处 你继承之后，直接就可以调用一大堆现成方法：

```Java
userService.save(user);
userService.getById(1L);
userService.page(page, queryWrapper);
```

不用自己写xml、不用写SQL。

### 3、那如果我不想继承 `ServiceImpl` 行不行？

✅ 完全可以！ 你可以不继承 `ServiceImpl`，自己写Service，自己注入Mapper手动调用：

```Java
@Service
public class UserServiceImpl implements UserService {

    @Autowired
    private UserMapper userMapper;

    @Override
    public User getById(Long id) {
        return userMapper.selectById(id);
    }
}
```

但是这样所有基础CRUD都要你自己手动封装，失去MP自带的便利，**业务里一般不这么干**。

### 4、配套的完整结构对照（整套MP三层）

```
User（实体类）
UserMapper extends BaseMapper<User>
UserService extends IService<User>
UserServiceImpl extends ServiceImpl<UserMapper, User> implements UserService
```

> `IService<T>` 是Service层的接口规范，里面定义了那些save、list、page这些方法； `ServiceImpl` 是这个接口的默认实现。

### 一句话总结

- MP开发标准套路：**Service实现类继承 `ServiceImpl<你的Mapper, 实体>`**
- 它是MP提供的通用实现，不是原生MyBatis的；
- 继承它 = 直接复用MP写好的全套基础增删改查。

### 补充小坑

> 注意：很多人搞混：
> 
> - `BaseMapper`：给Mapper用的
> - `ServiceImpl` + `IService`：给Service层用的
