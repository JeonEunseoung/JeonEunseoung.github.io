---
layout: post
title: 프로그래머스 >> GROUP BY >> 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기
subtitle: SQL
date: '2023-11-07 23:05:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기(MySQL)

<h2>문제 설명</h2>
다음은 어느 자동차 대여 회사에서 대여중인 자동차들의 정보를 담은 <b>CAR_RENTAL_COMPANY_CAR</b> 테이블입니다. <b>CAR_RENTAL_COMPANY_CAR</b> 테이블은 아래와 같은 구조로 되어있으며, <b>CAR_ID</b>, <b>CAR_TYPE</b>, <b>DAILY_FEE</b>, <b>OPTIONS</b> 는 각각 자동차 ID, 자동차 종류, 일일 대여 요금(원), 자동차 옵션 리스트를 나타냅니다.<br>
<table>
    <thead>
        <th>Column name</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>CAR_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>CAR_TYPE</td>
            <td>VARCHAR(255)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>DAILY_FEE</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>OPTIONS</td>
            <td>VARCHAR(255)</td>
            <td>FALSE</td>
        </tr>
    </tbody>
</table>
자동차 종류는 '세단', 'SUV', '승합차', '트럭', '리무진' 이 있습니다. 자동차 옵션 리스트는 콤마(',')로 구분된 키워드 리스트(옵션 리스트 값 예시: '열선시트', '스마트키', '주차감지센서')로 되어있으며, 키워드 종류는 '주차감지센서', '스마트키', '네비게이션', '통풍시트', '열선시트', '후방카메라', '가죽시트' 가 있습니다.<br>
<b>CAR_RENTAL_COMPANY_CAR</b> 테이블에서 '통풍시트', '열선시트', '가죽시트' 중 하나 이상의 옵션이 포함된 자동차가 자동차 종류 별로 몇 대인지 출력하는 SQL문을 작성해주세요. 이때 자동차 수에 대한 컬럼명은 <b>CARS</b>로 지정하고, 결과는 자동차 종류를 기준으로 오름차순 정렬해주세요.
<h2>코드</h2>
```sql
-- 자동차 종류 별 특정 옵션이 포함된 자동차 수 구하기
SELECT CAR_TYPE, COUNT(*) as CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE '%가죽시트%' OR OPTIONS LIKE '%통풍시트%' OR OPTIONS LIKE '%열선시트%'
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE

SELECT CAR_TYPE, COUNT(*) as CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS IN ('가죽시트', '통풍시트', '열선시트')
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE;
```
<br>


