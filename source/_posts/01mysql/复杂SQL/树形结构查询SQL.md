1. inner join 自连接 / left join似乎也可以？

2. WITH AS 递归查询
   ex:

   ```SQL
   with RECURSIVE t1 AS(
       SELECT 1 AS n
       union all
       SELECT n+1 FROM t1 WHERE n<5
   )
   SELECT * from t1
   ```

   ```SQL
   with recursive temp as (
   select * from  course_category p where  id= '1-1-1'
    union all
   select t.* from course_category t inner join temp on temp.parentid = t.id  
   //temp表是下次递归的基础
   )
   select *  from temp order by temp.id, temp.orderby
   ```

   