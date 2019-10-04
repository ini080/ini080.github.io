---
layout: post
title:  "DataBase (Join)"
subtitle:   "DB"
categories: Study
tags: DB
---
1. INNER JOIN

결합된 테이블에 조건의 내용이 공통으로 들어가 있는 값을 결과 집합으로 만들어준다. ON 다음에 들어가는 조건에 맞는 내용들만 보여주게 된다.


기본형식

SELECT 열 목록
   FROM 첫번째 테이블 [AS 별칭] INNER JOIN 두번째 테이블 [AS별칭]
       ON(join_condition)



SELECT 회원이름, 구매한도서, 작가, 구매시기
   FROM 회원정보 INNER JOIN 구매내역
 WHERE 회원이름 = '김군'



SELECT DISTINCT M.회원정보, M.회원이름, M.거주지역
   FROM 회원정보 AS M
   INNER JOIN 구매내역 AS B
       ON M.회원번호 = B.회원번호
 ORDER BY M.회원번호



SELECT M.회원이름, B.구매한도서, P.가격
  FROM 회원정보 AS M
  INNER JOIN 구매내역 AS B
      ON M.회원번호 = B.회원번호
  INNER JOIN 가격 AS P
      ON B.구매한도서 = P.구매한도서
 ORDER BY M.회원이름

2.  OUTER JOIN

INNER JOIN 문을 포함하고 한쪽에만 내용이 있더라도 지정한 기준 테이블에 있는 모든 데이터를 가져오는 조인방식

SELECT 열목록
   FROM 첫번째 테이블
   <LEFT | RIGHT | FULL> OUTER JOIN 두번째 테이블
       ON(join_condition)
   [WHERE 검색조건]


- LEFT OUTER JOIN
왼쪽 테이블이 기준이 되어서 그 테이블에 있는 데이터를 모두 가져온다. 기준으로 지정되지 않은 오른쪽 테이블에서 가져올 수 없는 열은 NULL로 표현된다.


SELECT M.회원이름, B.구매한도서, B.작가, B.구매시기
   FROM 회원정보 AS M
    LEFT OUTER JOIN 구매내역 AS B
      ON M.회원번호 = B.회원번호
 ORDER BY M.회원번호



- RIGHT OUTER JOIN
오른쪽 테이블이 기준이 되어서 그 테이블에 있는 데이터를 모두 가져온다. 기준으로 지정되지 않은 왼쪽 테이블에서 가져올 수 없는 열은 NULL로 표현된다.

SELECT B.구매한도서, B.작가, B.구매시기, M.회원이름
  FROM 회원정보 AS M
  RIGHT OUTER JOIN 구매내역 AS B
      ON M.회원번호 = B.회원번호
ORDER BY B.구매시기



- FULL OUTER JOIN
왼쪽과 오른쪽에 관계없이 조건이 일치하지 않아도 양쪽의 모든 내용을 포함해서 나타낸다.


SELECT M.회원이름, B.구매한 도서, B.작가, B.구매시기
   FROM 회원정보 AS M
    FULL OUTER JOIN 구매내역 AS B
 ORDER BY M.회원번호



3. SELF JOIN
하나의 테이블에 같은 데이터가 존재하는데 그 의미가 다르게 존재하는 경우. 즉, 같은 데이터이지만 다른 열에 있는 경우에는 두 테이블을 서로 SELF JOIN 문으로 확인가능


SELECT A.회원이름, A.주거지역, A.연락처, B.회원이름 AS 추천인, B.연락처
  FROM 회원정보 AS A
  INNER JOIN 회원정보 AS B
      ON A.추천한 회원 = B.회원번호
WHERE A.회원이름 = '김군'



![image](/assets/img/study/db/11.png)

출처: https://enspring.tistory.com/581
