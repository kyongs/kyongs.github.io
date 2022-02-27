---
title: "[C/C++] 자주쓰는 GDB 디버깅 명령어 정리"
updated: 2022-02-24 18"15
---

### gdb 실행

---

```shell
gdb
```

### gdb에 프로세스 붙이기

---

```shell
(gdb) attach {실행중인 프로세스 ID}
```

### gdb 종료

---

```shell
(gdb) [ctrl]+d #강제종료
```

### 소스 출력

---

1. main 함수 기점으로 소스 출력

```shell
(gdb) l
```

2. 이전 행 출력

```shell
(gdb) l-
```

3. 함수의 소스 출력

```shell
(gdb) l {함수명}
```

4. 한 번에 표시되는 라인 수(n) 설정

```shell
(gdb) set listsize {n}
```

### breakpoint

---

1.  breakpoint 목록 보기

```shell
(gdb) info b
```

2. breakpoint 설정

```shell
(gdb) b {함수명/라인수/*주소}
```

3. 1회만 break

```shell
(gdb) cl {함수명/행번호/파일명:함수명/*주소}
```

4. 모든 breakpoint 삭제

```shell
(gdb) d
```

5. breakpoint 비활성화

```shell
(gdb) disable {breakpoint 번호}
```

6. breakpoint 활성화

```shell
(gdb) enable {breakpoint 번호}
```

### 프로그램 진행

---

1. 실행

```shell
(gdb) r
```

2. 다음 breakpoint

```shell
(gdb) c
```

3.  call stack

```shell
(gdb) bt
```

4. 함수 호출 내부까지 들어가기

```shell
(gdb) s
```

5. 현재 행 실행 후 멈춤

```shell
(gdb) n
```

6. 현재 함수 끝난 시점으로 진행

```shell
(gdb) finish
```

7.  함수 진행 중 빠져나오기

```shell
(gdb) return {리턴값}
```

8. 현재 루프 빠져나가기

```shell
(gdb) u
```

9. instruction 단위 수행

```shell
(gdb) ni
```

10. instruction 단위 수행 (내부까지)

```shell
(gdb) si
```

### 변수

---

1.  지역변수 보기

```shell
(gdb) info locals
```

2.  전역변수 보기

```shell
(gdb) info variables
```

3.  변수 보기

```shell
(gdb) p {변수명}
```

4. 포인트 변수 보기

```shell
(gdb) p *{변수명}
```

5. 레지스터 전체 보기

```shell
(gdb) info all-registers
```

6. 레지스터 값 보기

```shell
(gdb) p ${레지스터명}
```
