#SQLPractice

语句练习：https://www.nowcoder.com/ta/sql

选课系统设计：https://www.cnblogs.com/1030351096zzz/p/6095057.html

**SQL1:**

select * from employees  order by hire_date desc limit 1;

select * from employees  order by hire_date desc limit 1 offset 0;偏移量为0

select * from employees  order by hire_date desc limit 0,1;从0开始，取一个

select * from employees where hire_date=(select max(hire_date) from employees);先选最大的入职日期，再查询具体信息

**SQL2:**

Select * from employees order by hire_date desc limit 2,1;

Select * from employees order by hire_date desc limit 1 offset 2;

Select * from employees where hire_date=(select distinct hire_date from employees order by hire_date desc limit 1 offset 2);子查询

select * from employees where hire_date=(select hire_date from employees group by hire_date order by hire_date desc limit 1 offset 2);子查询

**SQL3:**

select 

​    s.*,

​    d.dept_no 

from 

​    salaries s 

​    left join dept_manager d 

​      on s.emp_no=d.emp_no

where s.to_date='9999-01-01'and d.to_date='9999-01-01'

order by s.emp_no; 

**SQL4:**

Select e.last_name,e.first_name,d.dept_no from employees as e join dept_emp as d on e.emp_no=d.emp_no;

Select e.last_name,e.first_name,d.dept_no from employees as e,dept_emp as d where e.emp_no=d.emp_no;

Select e.last_name,e.first_name,d.dept_no from employees as e inner join dept_emp as d on e.emp_no=d.emp_no;

**SQL5:**

select e.last_name,e.first_name,d.dept_no from employees as e left outer join dept_emp as d on e.emp_no=d.emp_no;

**SQL7:**

Select emp_no,count(emp_no) as t from salaries group by emp_no having t>15;

**SQL8:**

Select distinct salary from salaries where to_date='9999-01-01' order by salary desc;//去重

select salary from salaries where to_date='9999-01-01' group by salary order by salary desc;//分组

**SQL10:**

Select emp_no from employees where emp_no not in(select emp_no from dept_manager);

Select e.emp_no from employees as e left join dept_manager as d on e.emp_no=d.emp_no where dept_no is null;//dept_no是领导特有的字段

**SQL11:**

Select e.emp_no,m.emp_no as manager_no from dept_emp as e inner join dept_manager as m on e.dept_no=m.dept_no where e.emp_no!=m.emp_no and e.to_date='9999-01-01' and m.to_date='9999-01-01';

**SQL12:**

select

   t1.dept_no,t2.emp_no,t1.salary

From

  (Select d.dept_no,max(s.salary) salary from dept_emp d join salaries s on d.emp_no=s.emp_no and d.to_date='9999-01-01' and s.to_date='9999-01-01' group by d.dept_no) t1

join

  (Select d.emp_no,d.dept_no,s.salary from dept_emp d join salaries s on d.emp_no=s.emp_no and d.to_date='9999-01-01' and s.to_date='9999-01-01')t2

on

  t1.dept_no=t2.dept_no and t1.salary=t2.salary

order by

 t1.dept_no;//dept_no和emp_no是无关联的，所以这两个字段也需要创建

order by 不能在group by之后使用，会打乱分组的顺序，每条记录的字段是分散的，在查询时可能会打乱。

![image-20210518155521496](/Users/duanxiangqing/Library/Application Support/typora-user-images/image-20210518155521496.png)



**SQL55:**

Select * from employees limit 5,5;

select * from employees limit 5 offset 5;