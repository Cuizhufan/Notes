



# SQL

select * from user_profile

select distinct * from user_profile 去重

例5.检索记录行 6-10

```sql
SELECT` `* ``FROM` `table` `LIMIT 5,5
```

例6.检索记录行 11-last

```sql
SELECT` `* ``FROM` `table` `LIMIT 10,-1
```

例7.检索前 5 个记录行

```sql
SELECT` `* ``FROM` `table` `LIMIT 5
```

![图片说明](https://uploadfiles.nowcoder.com/images/20210928/170531835_1632759782879/3211A9C2DBBEC176C7BFA1F02F91FB8B)

# 简单查询

```SQL
查询学校为北大
SELECT device_id,gender,age FROM user_profile WHERE university="北京大学"
查询年龄在20-23
SELECT device_id,gender,age FROM user_profile WHERE age BETWEEN 20 AND 23
查询复旦大学意外的所有信息
SELECT device_id,gender,age,university FROM user_profile WHERE university!="复旦大学"
年龄不为空
SELECT device_id,gender,age,university FROM user_profile WHERE age IS NOT NULL
gpa大于3.5 男性
SELECT device_id,gender,age,university,gpa FROM user_profile WHERE gpa>3.5 AND gender="male"
//gpa大于3.7或者北京大学
SELECT device_id,gender,age,university,gpa from user_profile where gpa>3.7 or university='北京大学'
//查找 集合 北大 复旦 山东大学
select device_id,gender,age,university,gpa from user_profile
where university in('北京大学','复旦大学','山东大学');
//and 优先级大于 or
SELECT device_id,gender,age,university,gpa from user_profile where (gpa>3.5 and university="山东大学") or (gpa>3.8 and university='复旦大学')
//like字符匹配  查找带有北京的大学
select device_id,age,universityfrom user_profile WHERE university like '%北京%' 
```

# 复杂查询

查最大 最小

```
//查找最大 order by xxx desc order by xxx asc 
select gpa from user_profile WHERE university='复旦大学' order by gpa desc limit 1
//或者 max（）
select max(gpa )from user_profile WHERE university='复旦大学'
```



```SQL
计算男生数量和平均gpa，avg（xxx）求平均 round（xxx,1）精度保留一位
select count(gender) as male_num,round(avg(gpa),1) as avg_gpa
from user_profile
where gender='male';
```

分组计算

不同的组别（情况）：university gender

计算的属性：用户数量，30天平均活跃度，平均发帖数量

```sql
SELECT gender,university,count(device_id) as user_num,avg(active_days_within_30),avg(question_cnt)
from user_profile
group by university,gender;
```

分组+条件过滤:   请取出平均发贴数低于5的学校或平均回帖数小于20的学校。

分组：学校

过滤属性：计算后的平均回帖数和发帖数

```sql
select university,avg(question_cnt) as avg_question,
avg(answer_cnt) as avg_answer_cont
from user_profile
group by university
having
avg_question<5
or
avg_answer_cont<20
```

分组排序：现在运营想要查看不同大学的用户平均发帖情况，并期望结果按照平均发帖情况进行升序排列

```sql
select university , avg( question_cnt) as avg_question_cnt
from user_profile
group by university order by avg_question_cnt asc
```





```SQL
select 学号, avg(成绩) as 平均成绩
from score
where 成绩 <60
group by 学号
having count(课程号)>2;
```



# 多表查询：

左连接两个表格

```sql
select t1.device_id,question_id,result
from question_practice_detail t1
left JOIN user_profile t2
on t1.device_id = t2.device_id
where university = '浙江大学'
```



# 添加数据：

```mysql
insert into student(学号,姓名,出生日期,性别) 
values('0001' , '猴子' , '1989-01-01' , '男');
```

我叫czf 就读于浙江工业大学控制工程专业硕士，我想应聘一份前端开发的岗位。

