---
layout: post
title: 프로그래머스 >> GROUP BY >> 년, 월, 성별 별 상품 구매 회원 수 구하기
subtitle: SQL
date: '2023-12-11 20:30:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 년, 월, 성별 별 상품 구매 회원 수 구하기(MySQL)

<h2>문제</h2>
다음은 어느 의류 쇼핑몰에 가입한 회원 정보를 담은 <b>USER_INFO</b> 테이블과 온라인 상품 판매 정보를 담은 <b>ONLINE_SALE</b> 테이블 입니다.<b>USER_INFO</b> 테이블은 아래와 같은 구조로 되어있으며 <b>USER_ID</b>, <b>GENDER</b>, <b>AGE</b>, <b>JOINED</b>는 각각 회원 ID, 성별, 나이, 가입일을 나타냅니다.
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>USER_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>GENDER</td>
            <td>TINYINT(1)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>AGE</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>JOINED</td>
            <td>DATE</td>
            <td>FALSE</td>
        </tr>
    </tbody>
</table>
<b>GENDER</b> 컬럼은 비어있거나 0 또는 1의 값을 가지며 0인 경우 남자를, 1인 경우는 여자를 나타냅니다.<br>
<b>ONLINE_SALE</b> 테이블은 아래와 같은 구조로 되어있으며, <b>ONLINE_SALE_ID</b>, <b>USER_ID</b>, <b>PRODUCT_ID</b>, <b>SALES_AMOUNT</b>, <b>SALES_DATE</b>는 각각 온라인 상품 판매 ID, 회원 ID, 상품 ID, 판매량, 판매일을 나타냅니다.<br>
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>ONLINE_SALE_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>USER_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>PRODUCT_ID</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>SALES_AMOUNT</td>
            <td>INTEGER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>SALES_DATE</td>
            <td>DATE</td>
            <td>FALSE</td>
        </tr>
    </tbody>
</table>
동일한 날짜, 회원 ID, 상품 ID 조합에 대해서는 하나의 판매 데이터만 존재합니다.<br>
<b>USER_INFO</b> 테이블과 <b>ONLINE_SALE</b> 테이블에서 년, 월, 성별 별로 상품을 구매한 회원수를 집계하는 SQL문을 작성해주세요. 결과는 년, 월, 성별을 기준으로 오름차순 정렬해주세요. 이때, 성별 정보가 없는 경우 결과에서 제외해주세요.<br>
<h2>코드</h2>
```sql
-- 년, 월, 성별 별 상품 구매 회원 수 구하기
SELECT YEAR(b.sales_date) as YEAR, MONTH(b.sales_date) as MONTH, a.GENDER as GENDER, COUNT(distinct a.USER_ID) as USERS
FROM USER_INFO as a JOIN ONLINE_SALE as b 
ON a.USER_ID=b.USER_ID
GROUP BY YEAR, MONTH, GENDER
HAVING GENDER IS NOT NULL
ORDER BY YEAR, MONTH, GENDER

SELECT DATE_FORMAT(b.sales_date,'%Y') as YEAR, DATE_FORMAT(b.sales_date,'%c') as MONTH, a.GENDER as GENDER, COUNT(distinct a.USER_ID) as USERS
FROM USER_INFO as a JOIN ONLINE_SALE as b 
ON a.USER_ID=b.USER_ID
GROUP BY YEAR, MONTH, GENDER
HAVING GENDER IS NOT NULL
ORDER BY YEAR, MONTH, GENDER
```
<h2>학습</h2>
YEAR(DATE), DATE_FORMAT(b.sales_date,'%Y')-> year만 표시<br>
MONTH(DATE), DATE_FORMAT(b.sales_date,'%c')-> month만 표시<br>
JOIN한 후에 count 쓸려면 해당 칼럼 distinct<br>
TINYINT는 데이터베이스에서 사용되는 정수형 데이터 유형 중 하나<br>
TINYINT는 작은 정수 값을 저장하는 데 유용하며, 주로 0에서 255까지의 값을 저장하는 데 사용될 수 있습니다.<br>
예를 들어, 성별 정보(남성 또는 여성)를 나타내기 위해 0 또는 1을 사용하는 경우, 혹은 특정 상태를 나타내는 데 작은 범위의 숫자가 필요한 경우에 TINYINT를 사용할 수 있습니다.<br>







