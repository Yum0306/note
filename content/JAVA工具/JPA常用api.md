## 自定义方法的实现:

Jpa本身还提供了一些自定义声明方法的规则，例如：在接口中使用关键字findBy、readBy、getBy作为方法名的前缀，拼接实体类中的属性字段（首字母大写），并可选择拼接一些SQL关键字来组合成一个查询方法，例如，对于用户实体，关键字可以这样使用
- 1.And，如：findByIdAndName(Long id, String name); 并且
- 2.Or,如：findByIdOrName(Long id, String name); 或者
- 3.Between,如：findByCreateDateBetween(Date start, Date end); 在之间
- 4.LessThan,如：findByCreateDateLessThan(Date start); 小于
- 5.GreaterThan,如：findByCreateDateGreaterThan(Date start); 大于
- 6.IsNull,如：findByNameIsNull(); 空
- 7.IsNotNull,与上等价 不等于空
- 8.Like,如：findByNameLike(String name); 模糊查询
- 9.NotLike:与上等价 不模糊
- 10.OrderBy,如：findByNameOrderByIdAsc(String name); 排序
- 11.Not,如：findByNameNot(String name); 不得于
- 12.In,如：findByNameIn(Collection<String> nameList); 在什么里面 数组
- 13.NotIn,与上等价。不在什么里面 数组
- 14.top/limit 查询方法结果的数量通过关键字限制 默认1，可以加数字指定返回最大结果
例如:
- User findFirstByOrderByLastnameAsc();
- User findTopByOrderByAgeDesc();
- Page<User> queryFirst10ByLastname(String lastname, Pageable pageable);
- Slice<User> findTop3ByLastname(String lastname, Pageable pageable);
- List<User> findFirst10ByLastname(String lastname, Sort sort);
- List<User> findTop10ByLastname(String lastname, Pageable pageable);
你同样可以写一个自定义的方法，使用@Query注解+HQL语句实现你想要的效果
  
## 


详细查询语法  
| 关键词              | 示例                                                         | 对应的sql片段                                             |  
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |  
| `And`               | `findByLastnameAndFirstname`                                 | `… where x.lastname = ?1 and x.firstname = ?2`               |  
| `Or`                | `findByLastnameOrFirstname`                                  | `… where x.lastname = ?1 or x.firstname = ?2`                |  
| `Is,Equals`         | `findByFirstname`,`findByFirstnameIs`,`findByFirstnameEquals` | `… where x.firstname = ?1`                                   |  
| `Between`           | `findByStartDateBetween`                                     | `… where x.startDate between ?1 and ?2`                      |  
| `LessThan`          | `findByAgeLessThan`                                          | `… where x.age < ?1`                                         |  
| `LessThanEqual`     | `findByAgeLessThanEqual`                                     | `… where x.age <= ?1`                                        |  
| `GreaterThan`       | `findByAgeGreaterThan`                                       | `… where x.age > ?1`                                         |  
| `GreaterThanEqual`  | `findByAgeGreaterThanEqual`                                  | `… where x.age >= ?1`                                        |  
| `After`             | `findByStartDateAfter`                                       | `… where x.startDate > ?1`                                   |  
| `Before`            | `findByStartDateBefore`                                      | `… where x.startDate < ?1`                                   |  
| `IsNull`            | `findByAgeIsNull`                                            | `… where x.age is null`                                      |  
| `IsNotNull,NotNull` | `findByAge(Is)NotNull`                                       | `… where x.age not null`                                     |  
| `Like`              | `findByFirstnameLike`                                        | `… where x.firstname like ?1`                                |  
| `NotLike`           | `findByFirstnameNotLike`                                     | `… where x.firstname not like ?1`                            |  
| `StartingWith`      | `findByFirstnameStartingWith`                                | `… where x.firstname like ?1` (parameter bound with appended `%`) |  
| `EndingWith`        | `findByFirstnameEndingWith`                                  | `… where x.firstname like ?1` (parameter bound with prepended `%`) |  
| `Containing`        | `findByFirstnameContaining`                                  | `… where x.firstname like ?1` (parameter bound wrapped in `%`) |  
| `OrderBy`           | `findByAgeOrderByLastnameDesc`                               | `… where x.age = ?1 order by x.lastname desc`                |  
| `Not`               | `findByLastnameNot`                                          | `… where x.lastname <> ?1`                                   |  
| `In`                | `findByAgeIn(Collection<Age> ages)`                          | `… where x.age in ?1`                                        |  
| `NotIn`             | `findByAgeNotIn(Collection<Age> ages)`                       | `… where x.age not in ?1`                                    |  
| `True`              | `findByActiveTrue()`                                         | `… where x.active = true`                                    |  
| `False`             | `findByActiveFalse()`                                        | `… where x.active = false`                                   |  
| `IgnoreCase`        | `findByFirstnameIgnoreCase`                                  | `… where UPPER(x.firstame) = UPPER(?1)`                      |
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjk1NTQ5NzAwLC0xODI4OTM3NzQ4XX0=
-->