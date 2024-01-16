---
layout: post
title: 프로그래머스 >> GROUP BY >> 즐겨찾기가 가장 많은 식당 정보 출력하기
subtitle: SQL
date: '2024-01-15 19:56:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 즐겨찾기가 가장 많은 식당 정보 출력하기(MySQL)

<h2>문제</h2>
다음은 식당의 정보를 담은 <b>REST_INFO</b> 테이블입니다. <b>REST_INFO</b> 테이블은 다음과 같으며 <b>REST_ID</b>, <b>REST_NAME</b>, <b>FOOD_TYPE</b>, <b>VIEWS</b>, <b>FAVORITES</b>, <b>PARKING_LOT</b>, <b>ADDRESS</b>, <b>TEL</b>은 식당 ID, 식당 이름, 음식 종류, 조회수, 즐겨찾기수, 주차장 유무, 주소, 전화번호를 의미합니다.<br>
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>REST_ID</td>
            <td>VARCHAR(5)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>REST_NAME</td>
            <td>VARCHAR(50)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>FOOD_TYPE</td>
            <td>VARCHAR(20)</td>
            <td>TRUE</td>
        </tr>
        <tr>
            <td>VIEWS</td>
            <td>NUMBER</td>
            <td>TRUE</td>
        </tr>
        <tr>
            <td>FAVORITES</td>
            <td>NUMBER</td>
            <td>TRUE</td>
        </tr>
        <tr>
            <td>PARKING_LOT</td>
            <td>VARCHAR(1)</td>
            <td>TRUE</td>
        </tr>
        <tr>
            <td>ADDRESS</td>
            <td>VARCHAR(100)</td>
            <td>TRUE</td>
        </tr>
        <tr>
            <td>TEL</td>
            <td>VARCHAR(100)</td>
            <td>TRUE</td>
        </tr>
    </tbody>
</table>
<b>REST_INFO</b> 테이블에서 음식종류별로 즐겨찾기수가 가장 많은 식당의 음식 종류, ID, 식당 이름, 즐겨찾기수를 조회하는 SQL문을 작성해주세요. 이때 결과는 음식 종류를 기준으로 내림차순 정렬해주세요.<br>
<h2>코드</h2>
```sql
-- 즐겨찾기가 가장 많은 식당 정보 출력하기
SELECT FOOD_TYPE, REST_ID, REST_NAME, FAVORITES
FROM REST_INFO
WHERE (FOOD_TYPE, FAVORITES) IN (SELECT FOOD_TYPE, MAX(FAVORITES) as FAVORITES FROM REST_INFO GROUP BY FOOD_TYPE)
ORDER BY FOOD_TYPE DESC
```
<h2>학습</h2>
GROUP BY가 들어간 서브 쿼리문은 주로 WHERE 절에서 조건 비교를 할 때 많이 쓰인다.<br>







