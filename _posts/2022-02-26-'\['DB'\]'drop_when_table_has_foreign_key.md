---
title: "[DB] 외래키가 존재하는 테이블 삭제하기"
updated: 2022-02-24 18"15
---

```sql
set FOREIGN_KEY_CHECK = 0;
drop table XXX;
set FOREIGN_KEY_CHECKS=1; # 다시 돌려놓기

```
