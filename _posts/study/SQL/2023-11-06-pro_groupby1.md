---
layout: post
title: 프로그래머스 >> GROUP BY >> 성분으로 구분한 아이스크림 총 주문량
subtitle: SQL
date: '2023-11-06 21:15:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 성분으로 구분한 아이스크림 총 주문량(MySQL)

<h2>문제 설명</h2>
다음은 아이스크림 가게의 상반기 주문 정보를 담은 <b>FIRST_HALF</b> 테이블과 아이스크림 성분에 대한 정보를 담은 <b>ICECREAM_INFO</b> 테이블입니다. <b>FIRST_HALF</b> 테이블 구조는 다음과 같으며, <b>SHIPMENT_ID</b>, <b>FLAVOR</b>, <b>TOTAL_ORDER</b> 는 각각 아이스크림 공장에서 아이스크림 가게까지의 출하 번호, 아이스크림 맛, 상반기 아이스크림 총주문량을 나타냅니다. <b>FIRST_HALF</b> 테이블의 기본 키는 <b>FLAVOR</b>입니다.<br>
<table>
    <thead>
        <th>NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>SHIPMENT_ID</td>
            <td>INT(N)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>FLAVOR</td>
            <td>VARCHAR(N)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>TOTAL_ORDER</td>
            <td>INT(N)</td>
            <td>FALSE</td>
        </tr>
    </tbody>
</table>
ICECREAM_INFO 테이블 구조는 다음과 같으며, FLAVOR, INGREDITENT_TYPE 은 각각 아이스크림 맛, 아이스크림의 성분 타입을 나타냅니다. INGREDIENT_TYPE에는 아이스크림의 주 성분이 설탕이면 sugar_based라고 입력되고, 아이스크림의 주 성분이 과일이면 fruit_based라고 입력됩니다. ICECREAM_INFO의 기본 키는 FLAVOR입니다. ICECREAM_INFO테이블의 FLAVOR는 FIRST_HALF 테이블의 FLAVOR의 외래 키입니다.<br>
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Type</th>
            <th>Nullable</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>FLAVOR</td>
            <td>VARCHAR(N)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>INGREDIENT_TYPE</td>
            <td>VARCHAR(N)</td>
            <td>FALSE</td>
        </tr>
    </tbody>
</table>
상반기 동안 각 아이스크림 성분 타입과 성분 타입에 대한 아이스크림의 총주문량을 총주문량이 작은 순서대로 조회하는 SQL 문을 작성해주세요. 이때 총주문량을 나타내는 컬럼명은 TOTAL_ORDER로 지정해주세요.<br>
<h2>코드</h2>
```sql
-- 성분으로 구분한 아이스크림 총 주문량
SELECT b.INGREDIENT_TYPE INGREDIENT_TYPE, SUM(a.TOTAL_ORDER) as TOTAL_ORDER
FROM FIRST_HALF as a JOIN ICECREAM_INFO as b
WHERE a.flavor= b.flavor
GROUP BY b.INGREDIENT_TYPE
```
<br>


