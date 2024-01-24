---
layout: post
title: 프로그래머스 >> GROUP BY >> 저자 별 카테고리 별 매출액 집계하기
subtitle: SQL
date: '2024-01-24 21:04:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 저자 별 카테고리 별 매출액 집계하기(MySQL)

<h2>문제</h2>
다음은 어느 한 서점에서 판매중인 도서들의 도서 정보(<b>BOOK</b>), 저자 정보(<b>AUTHOR</b>) 테이블입니다.<br>
<b>BOOK</b> 테이블은 각 도서의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.<br>
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
        <th>Description</th>
    </thead>
    <tbody>
        <tr>
            <td>BOOK_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
            <td>도서 ID</td>
        </tr>
        <tr>
            <td>CATEGORY</td>
            <td>VARCHAR(N)</td>
            <td>FALSE</td>
            <td>카테고리 (경제, 인문, 소설, 생활, 기술)</td>
        </tr>
        <tr>
            <td>AUTHOR_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
            <td>저자 ID</td>
        </tr>
        <tr>
            <td>PRICE</td>
            <td>INTEGER</td>
            <td>FALSE</td>
            <td>판매가 (원)</td>
        </tr>
        <tr>
            <td>PUBLISHED_DATE</td>
            <td>DATE</td>
            <td>FALSE</td>
            <td>출판일</td>
        </tr>
    </tbody>
</table>
<b>AUTHOR</b> 테이블은 도서의 저자의 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.<br>
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
        <th>Description</th>
    </thead>
    <tbody>
        <tr>
            <td>AUTHOR_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
            <td>저자 ID</td>
        </tr>
        <tr>
            <td>AUTHOR_NAME</td>
            <td>VARCHAR(N)</td>
            <td>FALSE</td>
            <td>저자명</td>
        </tr>
    </tbody>
</table>
<b>BOOK_SALES</b> 테이블은 각 도서의 날짜 별 판매량 정보를 담은 테이블로 아래와 같은 구조로 되어있습니다.<br>
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
        <th>Description</th>
    </thead>
    <tbody>
        <tr>
            <td>BOOK_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
            <td>도서 ID</td>
        </tr>
        <tr>
            <td>SALES_DATE</td>
            <td>DATE</td>
            <td>FALSE</td>
            <td>판매일</td>
        </tr>
        <tr>
            <td>SALES</td>
            <td>INTEGER</td>
            <td>FALSE</td>
            <td>판매량</td>
        </tr>
    </tbody>
</table>
<b>2022년 1월</b>의 도서 판매 데이터를 기준으로 저자 별, 카테고리 별 매출액(<b>TOTAL_SALES = 판매량 * 판매가</b>) 을 구하여, 저자 ID(<b>AUTHOR_ID</b>), 저자명(<b>AUTHOR_NAME</b>), 카테고리(<b>CATEGORY</b>), 매출액(<b>SALES</b>) 리스트를 출력하는 SQL문을 작성해주세요.<br>
결과는 저자 ID를 오름차순으로, 저자 ID가 같다면 카테고리를 내림차순 정렬해주세요.<br>
<h2>코드</h2>
```sql
-- 저자 별 카테고리 별 매출액 집계하기
SELECT a.AUTHOR_ID,b.AUTHOR_NAME,a.CATEGORY, SUM((c.SALES*a.PRICE)) as TOTAL_SALES
FROM BOOK as a 
JOIN AUTHOR as b ON a.AUTHOR_ID=b.AUTHOR_ID
JOIN BOOK_SALES as c ON a.BOOK_ID=c.BOOK_ID
WHERE c.SALES_DATE LIKE '2022-01-%'
GROUP BY a.AUTHOR_ID, a.CATEGORY
ORDER BY a.AUTHOR_ID, a.CATEGORY DESC
```
<h2>학습</h2>
FROM 테이블 JOIN 테이블 JOIN 테이블 가능<br>
GROUP BY 했다면 집계함수를 활용하자<br>







