---
layout: post
title: 프로그래머스 >> GROUP BY >> 조건에 맞는 사용자와 총 거래금액 조회하기
subtitle: SQL
date: '2024-01-17 22:42:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 즐겨찾기가 가장 많은 식당 정보 출력하기(MySQL)

<h2>문제</h2>
다음은 중고 거래 게시판 정보를 담은 <b>USED_GOODS_BOARD</b> 테이블과 중고 거래 게시판 사용자 정보를 담은 <b>USED_GOODS_USER</b> 테이블입니다. <b>USED_GOODS_BOARD</b> 테이블은 다음과 같으며 <b>BOARD_ID</b>, <b>WRITER_ID</b>, <b>TITLE</b>, <b>CONTENTS</b>, <b>PRICE</b>, <b>CREATED_DATE</b>, <b>STATUS</b>, <b>VIEWS</b>는 게시글 ID, 작성자 ID, 게시글 제목, 게시글 내용, 가격, 작성일, 거래상태, 조회수를 의미합니다.
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>BOARD_ID</td>
            <td>VARCHAR(5)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>WRITER_ID</td>
            <td>VARCHAR(50)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>TITLE</td>
            <td>VARCHAR(100)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>CONTENTS</td>
            <td>VARCHAR(1000)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>PRICE</td>
            <td>NUMBER</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>CREATED_DATE</td>
            <td>DATE</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>STATUS</td>
            <td>VARCHAR(10)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>VIEWS</td>
            <td>NUMBER</td>
            <td>TRUE</td>
        </tr>
    </tbody>
</table>
<b>USED_GOODS_USER</b> 테이블은 다음과 같으며 <b>USER_ID</b>, <b>NICKNAME</b>, <b>CITY</b>, <b>STREET_ADDRESS1</b>, <b>STREET_ADDRESS2</b>, <b>TLNO</b>는 각각 회원 ID, 닉네임, 시, 도로명 주소, 상세 주소, 전화번호를 를 의미합니다.<br>
<table>
    <thead>
        <th>COLUMN NAME</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>USER_ID</td>
            <td>VARCHAR(50)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>NICKANME</td>
            <td>VARCHAR(100)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>CITY</td>
            <td>VARCHAR(100)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>STREET_ADDRESS1</td>
            <td>VARCHAR(100)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>STREET_ADDRESS2</td>
            <td>VARCHAR(100)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>TLNO</td>
            <td>VARCHAR(20)</td>
            <td>FALSE</td>
        </tr>
    </tbody>
</table>
<b>USED_GOODS_BOARD</b>와 <b>USED_GOODS_USER</b> 테이블에서 완료된 중고 거래의 총금액이 70만 원 이상인 사람의 회원 ID, 닉네임, 총거래금액을 조회하는 SQL문을 작성해주세요. 결과는 총거래금액을 기준으로 오름차순 정렬해주세요.<br>
<h2>코드</h2>
```sql
-- 조건에 맞는 사용자와 총 거래금액 조회하기
SELECT b.USER_ID, NICKNAME, SUM(PRICE) as TOTAL_SALES
FROM USED_GOODS_BOARD as a JOIN USED_GOODS_USER as b ON a.WRITER_ID=b.USER_ID
WHERE STATUS='DONE'
GROUP BY b.USER_ID
HAVING SUM(PRICE)>=700000
ORDER BY TOTAL_SALES ASC
```
<h2>학습</h2>
HAVING 은 집계함수 칼럼에 대해 조건을 걸 때 사용, WHERE 과 함께 사용 가능<br>







