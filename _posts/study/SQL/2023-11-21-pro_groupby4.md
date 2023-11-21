---
layout: post
title: 프로그래머스 >> GROUP BY >> 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기
subtitle: SQL
date: '2023-11-21 20:10:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기(MySQL)

<h2>문제 설명</h2>
다음은 어느 자동차 대여 회사의 자동차 대여 기록 정보를 담은 <b>CAR_RENTAL_COMPANY_RENTAL_HISTORY</b> 테이블입니다. <b>CAR_RENTAL_COMPANY_RENTAL_HISTORY</b> 테이블은 아래와 같은 구조로 되어있으며, <b>HISTORY_ID</b>, <b>CAR_ID</b>, <b>START_DATE</b>, <b>END_DATE</b> 는 각각 자동차 대여 기록 ID, 자동차 ID, 대여 시작일, 대여 종료일을 나타냅니다.
<table>
    <thead>
        <th>Column name</th>
        <th>Type</th>
        <th>Nullable</th>
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
<b>CAR_RENTAL_COMPANY_RENTAL_HISTORY</b> 테이블에서 2022년 10월 16일에 대여 중인 자동차인 경우 '대여중' 이라고 표시하고, 대여 중이지 않은 자동차인 경우 '대여 가능'을 표시하는 컬럼(컬럼명:<b> AVAILABILITY</b>)을 추가하여 자동차 ID와 <b>AVAILABILITY</b> 리스트를 출력하는 SQL문을 작성해주세요. 이때 반납 날짜가 2022년 10월 16일인 경우에도 '대여중'으로 표시해주시고 결과는 자동차 ID를 기준으로 내림차순 정렬해주세요.<br>
<h2>코드</h2>
```sql
-- 자동차 대여 기록에서 대여중 / 대여 가능 여부 구분하기
SELECT CAR_ID, 
    CASE WHEN CAR_ID IN (SELECT CAR_ID FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY WHERE '2022-10-16' BETWEEN START_DATE AND END_DATE) THEN '대여중'
    ELSE '대여 가능'
    END AS AVAILABILITY
FROM CAR_RENTAL_COMPANY_RENTAL_HISTORY
GROUP BY CAR_ID
ORDER BY CAR_ID DESC
```
<br>
<h2>학습</h2>
<b>BETWEEN '날짜' AND '날짜+1'</b> : 마지막 인덱스는 제외한 날짜 포함<br>
<b>HAVING</b>은 GROUP BY로 집계한 칼럼에 대한 조건절<br>
alter table 말고 칼럼과 값 할당 시, <b>CASE WHEN (조건) THEN '값' ~ ELSE '값' END</b> 절 사용 가능<br>


