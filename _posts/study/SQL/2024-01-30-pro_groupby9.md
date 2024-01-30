---
layout: post
title: 프로그래머스 >> GROUP BY >> 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기
subtitle: SQL
date: '2024-01-30 20:38:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기(MySQL)

<h2>문제</h2>
다음은 어느 자동차 대여 회사의 자동차 대여 기록 정보를 담은 <b>CAR_RENTAL_COMPANY_RENTAL_HISTORY</b> 테이블입니다. <b>CAR_RENTAL_COMPANY_RENTAL_HISTORY</b> 테이블은 아래와 같은 구조로 되어있으며, <b>HISTORY_ID</b>, <b>CAR_ID</b>, <b>START_DATE</b>, <b>END_DATE</b> 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.<br>
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>HISTORY_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>CAR_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>START_DATE</td>
            <td>DATE</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>END_DATE</td>
            <td>DATE</td>
            <td>FALSE</td>
        </tr>
    </tbody>
</table>
<b>CAR_RENTAL_COMPANY_RENTAL_HISTORY</b> 테이블에서 대여 시작일을 기준으로 2022년 8월부터 2022년 10월까지 총 대여 횟수가 5회 이상인 자동차들에 대해서 해당 기간 동안의 월별 자동차 ID 별 총 대여 횟수(컬럼명: <b>RECORDS</b>) 리스트를 출력하는 SQL문을 작성해주세요. 결과는 월을 기준으로 오름차순 정렬하고, 월이 같다면 자동차 ID를 기준으로 내림차순 정렬해주세요. 특정 월의 총 대여 횟수가 0인 경우에는 결과에서 제외해주세요.<br>
<h2>코드</h2>
```sql
-- 대여 횟수가 많은 자동차들의 월별 대여 횟수 구하기
SELECT MONTH(START_DATE) as MONTH,CAR_ID,COUNT(HISTORY_ID) as RECORDS
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
WHERE DATE_FORMAT(START_DATE,'%Y-%m') BETWEEN '2022-08' AND '2022-10'
AND CAR_ID IN (SELECT CAR_ID
                FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
                WHERE DATE_FORMAT(START_DATE,'%Y-%m') BETWEEN '2022-08' AND '2022-10'
                GROUP BY CAR_ID
                HAVING COUNT(history_id)>=5)
GROUP BY MONTH(START_DATE),CAR_ID
ORDER BY MONTH, CAR_ID DESC
```
<h2>학습</h2>
DATE_FORMAT(칼럼,'형식') -> %Y = yyyy, %m=mm<br>
BETWEEN 'string_date' AND 'string_date' 가능<br>
WHERE 절에서 서브쿼리문 적극 활용해보자<br>







