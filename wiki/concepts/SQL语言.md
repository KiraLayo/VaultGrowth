---
type: concept
domain: 技术
tags: [软考, 系统分析师, 数据库, SQL, 计算题]
created: 2026-08-04
updated: 2026-08-04
sources: ["[[wiki/sources/3.5非关系数据库-反规范化-SQL语言]]", "[[wiki/sources/课件总结-第三章]]"]
summary: "SQL 语言：DDL（几乎不考）、DML 必考（SELECT 三段式、GROUP BY/HAVING、聚合、LIKE、ORDER BY）；关系代数↔SQL 转换是综合考点。"
status: 成长中
mastery: 待复习
---

# SQL 语言

> 考试**不需要编程**，"只需要你能看懂"；有任意语言基础即可。**DML 要认真掌握，DDL 几乎没考过**（老师明确）。关系代数 ↔ SQL 互相转换是综合考点。

## DDL（定义，几乎不考）

```sql
CREATE TABLE S (
  SNO CHAR(5) NOT NULL UNIQUE,   -- 主键：非空、唯一
  SNAME CHAR(30) UNIQUE,
  STATUS CHAR(8), CITY CHAR(20),
  PRIMARY KEY (SNO));
```
ALTER（加列 ADD）/ DROP、CREATE UNIQUE INDEX（索引=目录）、CREATE VIEW（视图）

## DML（必考）

**SELECT 三段式**：`SELECT 列 FROM 表 WHERE 条件`（WHERE 可省略；多表 FROM 中间**加逗号**）

- 聚合：**AVG / MAX / MIN**（课件补 SUM / COUNT）；分组：**GROUP BY 分组 HAVING 分组后过滤**
- AS 改名、DISTINCT 去重、ORDER BY 排序（默认升序，降序 DESC）
- LIKE：**% 任意多个字符，_ 任意单个字符**（`'a_'`=两个字符以 a 开头；`'a%'`=以 a 开头任意长）
- INSERT INTO ... VALUES（每列都要插，可 NULL，**主键不能 NULL**）、DELETE FROM ... WHERE、UPDATE ... SET ... WHERE
- 集合运算：UNION（并）/ INTERSECT（交）/ MINUS（差）

## 真题演练

> **真题 1（零件关系 P 综合）**：P(零件号, 零件名称, 供应商号, 供应商所在地, 库存量)。
> ① 候选键 = 零件号+供应商号（联合），零件号/供应商号各能决定非主属性 → 部分依赖 → **1NF**。
> ② SELECT 零件号, **AVG(库存量) AS 平均库存量, MAX(库存量)-MIN(库存量) AS 差值**（选 A）。
> ③ FROM P、无 WHERE、**GROUP BY 零件号**（选 D）——"凡是看到聚合函数，后面肯定要分组"；SELECT 的列必须与分组列一致。

> **真题 2（自然连接↔SQL，C A D B）**：R(A,B,C,D,E) ⋈ S(B,C,F,G)。
> ① 列数：BC 重复去掉 → **7 列**（选 C）。
> ② SELECT R.A, R.C, S.F, S.G（投影选列，对应第 1/3/6/7 列，选 A）。
> ③ FROM R, S（逗号分隔，选 D）。
> ④ WHERE R.B=S.B AND R.C=S.C AND R.C<S.F——SQL 默认**笛卡尔积**，自然连接需显式转换；条件间 **AND 不是 OR**（选 B）。

> **课堂示例**：`SELECT SNO, AVG(SCORE) FROM STUDENT GROUP BY SNO HAVING AVG(SCORE) > 60`——按 SNO 分组才能查 SNO，"按别的来分，查 SNO 是查不到的"。

## 常见坑

- **GROUP BY 最坑**：SELECT 的列必须与分组列一致（单列分组时只能查该列+聚合函数）；**见到聚合函数必然要 GROUP BY**
- FROM 多表中间**加逗号**
- **SQL 默认笛卡尔积**，自然连接需 `R.B=S.B AND R.C=S.C` 显式转换；条件之间是 **AND**
- 关系代数↔SQL：投影=选列、选择=选行；列号对应列名（第 3 列= C、第 6 列=F → `R.C < S.F`）
- 自然连接重复列只显一次；LIKE：% 任意多个、_ 单个
- INSERT 每列都要插；主键不能为 NULL
- 数字不加引号、字符加引号（与关系代数一致）

## 相关页面

- 运算基础：[[wiki/concepts/关系代数]] · 范式：[[wiki/concepts/函数依赖与范式]]
- 来源：[[wiki/sources/3.5非关系数据库-反规范化-SQL语言]] · [[wiki/sources/课件总结-第三章]]
