---
title: 0常用SQL
date: 2026-01-28 11:52:13
updated: 2026-08-30 17:43:59
---

## 数据备份
``` mysqldump -uroot  -p123456 -d databsename tablename > /path/to/mytable.sql``` 



查询导出

```shell
mysql -udjg -p -Dlz_user_center_test \
--batch --raw --silent \
-e "
select
 ti.pk_id 'identityId',
 tu.pk_id 'userId',
 tu.phone 'account',
 tu.desensitization_phone 'desensitizationPhone',
 ti.identity_name 'teacherName',
 ti.state 'state',
 group_concat(tjd.duty_type) 'dutyType',
 tu.acceptance_status 'acceptanceStatus',
 ti.create_time 'createTime',
 ti.enable_state 'enableState',
 ti.org_name 'orgName',
 ti.org_id 'orgId',
 ti.ic_card 'icCard',
 tu.sex 'sex',
 ti.user_no 'userNo',
 cu.campus_id,
 cu.campus_name,
 bu.branch_id,
 bu.branch_name
from t_identity ti
join t_user tu on ti.user_id = tu.pk_id
left join t_job_duty tjd on tjd.identity_id = ti.pk_id
left join t_org_campus_user_relation cu on cu.identity_id = ti.pk_id
left join t_org_branch_user_relation bu on bu.identity_id = ti.pk_id
where ti.identity_type in (1,2,5)
  and ti.del_flag = '0'
  and ti.org_id = '1779772475219144704'
group by ti.pk_id
order by ti.create_time
" | sed 's/\t/,/g' > teacher_useaccount.csv

```













## 查询

### ORDER BY FIELD() 列按照指定值排序

``SELECT * FROM table_name ORDER BY FIELD(column_name, 'value1', 'value2', 'value3', ...);``

这里，*column_name*是要排序的字段，*'value1'*, *'value2'*, *'value3'*, ... 是自定义的排序顺序。如果*column_name*中的值不在列表中，则这些值会被放在结果集的最前面或最后面，取决于是否使用了DESC关键字。

例如，假设有一个员工表，包含员工姓名和部门信息，现在需要按照特定的部门顺序列出员工，可以这样写：

SELECT * FROM employees ORDER BY FIELD(department, 'HR', 'IT', 'Finance');

在这个例子中，属于'HR'部门的员工会首先列出，然后是'IT'部门的员工，接着是'Finance'部门的员工，其他部门的员工将按照他们在表中原本的顺序排列。如果是默认ASC, 不在这三者中的值会优先排在前面, 使用DESC排序的顺序是Finance, IT, HR, 其他。


## COALESCE(SUM(amount), 0)

## group_concat

## find_in_set

