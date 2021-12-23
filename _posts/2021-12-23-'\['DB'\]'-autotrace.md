---
title: "[DB] autotrace란?"
updated: 2021-12-23 23:17
---

## autotrace

SQL DML문이 정상적으로 실행된 후에 자동으로 SQL 옵티마이저에 의해 사용되는 실행계획과 실행 통계에 대한 정보를 얻을 수 있음.<br/>
SQL 성능 모니터링과 튜닝에 유용

**종류**
<br/>
`SET AUTOTRACE OFF` (default): 쿼리는 정상적으로 실행되지만 보고서는 생성되지 않음<br/>
`SET AUTOTRACE ON EXPLAIN`: 쿼리 정상 실행, AUTOTRACE 보고서에는 옵티마이저의 실행경로만 나타냄<br/>
`SET AUTOTRACE ON STATISTICS`: 쿼리 정상 실행, AUTOTRACE 보고서에는 SQL문의 실행 통계만 나타냄<br/>
`SET AUTOTRACE ON`: 쿼리 정상 실행, 보고서에 옵티마이저 실행경로와 SQL문의 실행 통계 모두 포함<br/>
`SET AUTOTRACE TRACEONLY`: SET AUTOTRACE ON과 비슷하지만 사용자의 쿼리 출력을 인쇄하지 않는다(무슨 소리인지 모르겠다 🤷‍♀️) <br/>
`SET AUTOTRACE TRACEONLY STATISTICS`: SET AUTOTRACE TRACEONLY에서 쿼리 계획을 표시하지 않음<br/>
`SET AUTOTRACE TRACEONLY EXPLAIN`: 쿼리 실제 수행 안함, SET AUTOTRACE TRACEONLY에서 통계 표시 생략
