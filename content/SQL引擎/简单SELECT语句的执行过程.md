---
# Title, summary, and page position.
title: 简单SELECT语句的执行过程
linktitle: 简单SELECT语句的执行过程
summary: 简单SELECT语句的执行过程
weight: 1
# icon: book
# icon_pack: fas

# Page metadata.
date: '2022-06-16T00:00:00Z'
type: book # Do not modify.
toc: true
---

# 概述

首先创建表

```sql
CREATE TABLE warehouse
(
    w_id SMALLINT PRIMARY KEY,
    w_name VARCHAR(10) NOT NULL,
    w_street_1 VARCHAR(20) CHECK(LENGTH(w_street_1)<>0),
    w_street_2 VARCHAR(20) CHECK(LENGTH(w_street_2)<>0),
    w_city VARCHAR(20),
    w_state CHAR(2) DEFAULT 'CN',
    w_zip CHAR(9),
    w_tax DECIMAL(4,2),
    w_ytd DECIMAL(12,2)
);
```

以`SELECT w_name FROM warehouse WHERE w_no = 1`为例说明SQL的查询过程

# 词法分析

openGauss采用了[Flex](https://www.geeksforgeeks.org/flex-fast-lexical-analyzer-generator/)做lexical anaysis。

在源码
