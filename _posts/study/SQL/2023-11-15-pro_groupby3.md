---
layout: post
title: 프로그래머스 >> GROUP BY >> 진료과별 총 예약 횟수 출력하기
subtitle: SQL
date: '2023-11-15 20:46:51 +0900'
categories: study
tags: SQL
comments: true
published: true
---
## 프로그래머스 >> GROUP BY >> 진료과별 총 예약 횟수 출력하기(MySQL)

<h2>문제 설명</h2>
다음은 종합병원의 진료 예약정보를 담은 <b>APPOINTMENT</b> 테이블 입니다.<br>
<b>APPOINTMENT</b> 테이블은 다음과 같으며 <b>APNT_YMD</b>, <b>APNT_NO</b>, <b>PT_NO</b>, <b>MCDP_CD</b>, <b>MDDR_ID</b>, <b>APNT_CNCL_YN</b>, <b>APNT_CNCL_YMD</b>는 각각 진료예약일시, 진료예약번호, 환자번호, 진료과코드, 의사ID, 예약취소여부, 예약취소날짜를 나타냅니다.<br>
<table>
    <thead>
        <th>Column name</th>
        <th>TYPE</th>
        <th>NULLABLE</th>
    </thead>
    <tbody>
        <tr>
            <td>APNT_YMD</td>
            <td>TIMESTAMP</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>APNT_NO</td>
            <td>NUMBER(5)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>PT_NO</td>
            <td>VARCHAR(10)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>MCDP_CD</td>
            <td>VARCHAR(6)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>MDDR_ID</td>
            <td>VARCHAR(10)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>APNT_CNCL_YN</td>
            <td>VARCHAR(1)</td>
            <td>FALSE</td>
        </tr>
        <tr>
            <td>APNT_CNCL_YMD</td>
            <td>DATE</td>
            <td>FALSE</td>
        </tr>
    </tbody>
</table>
<b>APPOINTMENT</b> 테이블에서 2022년 5월에 예약한 환자 수를 진료과코드 별로 조회하는 SQL문을 작성해주세요. 이때, 컬럼명은 '진료과 코드', '5월예약건수'로 지정해주시고 결과는 진료과별 예약한 환자 수를 기준으로 오름차순 정렬하고, 예약한 환자 수가 같다면 진료과 코드를 기준으로 오름차순 정렬해주세요.<br>
<h2>코드</h2>
```sql
-- 진료과별 총 예약 횟수 출력하기
SELECT MCDP_CD as '진료과코드', COUNT(*) as '5월예약건수'
FROM APPOINTMENT
WHERE APNT_YMD BETWEEN DATE('2022-05-01') AND DATE('2022-06-01')
GROUP BY MCDP_CD
ORDER BY COUNT(*), MCDP_CD

SELECT MCDP_CD as '진료과코드', COUNT(*) as '5월예약건수'
FROM APPOINTMENT
WHERE APNT_YMD LIKE '2022-05-%'
GROUP BY MCDP_CD
ORDER BY COUNT(*), MCDP_CD
```
<br>


