# SQLPractice

语句练习：https://www.nowcoder.com/ta/sql

选课系统设计：https://www.cnblogs.com/1030351096zzz/p/6095057.html

1. select * from employees  order by hire_date desc limit 1;

   select * from employees  order by hire_date desc limit 1 offset 0;偏移量为0

   select * from employees  order by hire_date desc limit 0,1;从0开始，取一个

   select * from employees where hire_date=(select max(hire_date) from employees);先选最大的入职日期，再查询具体信息

2. Select * from employees order by hire_date desc limit 2,1;

   Select * from employees order by hire_date desc limit 1 offset 2;

   Select * from employees where hire_date=(select distinct hire_date from employees order by hire_date desc limit 1 offset 2);子查询

   select * from employees where hire_date=(select hire_date from employees group by hire_date order by hire_date desc limit 1 offset 2);子查询

3. ???

4. Select e.last_name,e.first_name,d.dept_no from employees as e join dept_emp as d on e.emp_no=d.emp_no;

   Select e.last_name,e.first_name,d.dept_no from employees as e,dept_emp as d where e.emp_no=d.emp_no;

   Select e.last_name,e.first_name,d.dept_no from employees as e inner join dept_emp as d on e.emp_no=d.emp_no;

5. ???

6. 55

   Select * from employees limit 5,5;

   select * from employees limit 5 offset 5;
