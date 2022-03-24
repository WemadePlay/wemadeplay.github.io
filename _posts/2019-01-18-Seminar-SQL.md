---
layout: post
title: '2019년 1월 18일 완전 초보 SQL 세미나'
author: woohyuk.park
date: 2019-01-18 17:00 +0900
categories: [SEMINAR]
tags: [SQL]
image: /files/covers/seminar-sql-20190118.jpg
---

> 게임의 방향성을 결정하기 위해서 기획자들은 항상 데이터에 목말라 있습니다.
> 
> 기획자들이 원하는 데이터를 원하는 때에 언제든 확인할 수 있도록 박우혁님이 완전 초보 SQL 세미나를 준비해 주셨습니다.

![01](/files/images/2019-01-18-Seminar-SQL/01.jpg)

![02](/files/images/2019-01-18-Seminar-SQL/02.jpg)

![03](/files/images/2019-01-18-Seminar-SQL/03.jpg)

![04](/files/images/2019-01-18-Seminar-SQL/04.jpg)

![05](/files/images/2019-01-18-Seminar-SQL/05.jpg)

![06](/files/images/2019-01-18-Seminar-SQL/06.jpg)

이번 세미나의 목표는 기존에 생성되어 있는 데이터들을 이용하여 내가 보고 싶은 통계를 직접 뽑아볼 수 있는 방법을 알려드리는 것입니다.

![07](/files/images/2019-01-18-Seminar-SQL/07.jpg)

![08](/files/images/2019-01-18-Seminar-SQL/08.jpg)

![09](/files/images/2019-01-18-Seminar-SQL/09.jpg)

![10](/files/images/2019-01-18-Seminar-SQL/10.jpg)

Database는 테이블들의 모임입니다.

테이블은 세로 - 속성(Column)을 가진 가로 - 데이터(Row) 들의 집합입니다.

각 테이블들은 서로 연관성을 갖고 있을 수도 있습니다.

![11](/files/images/2019-01-18-Seminar-SQL/11.jpg)

각 테이블의 속성(Column)들 간에는 서로 연관성을 갖습니다.

![12](/files/images/2019-01-18-Seminar-SQL/12.jpg)

![13](/files/images/2019-01-18-Seminar-SQL/13.jpg)

위 구문은 기본적인 쿼리 형식으로, 해당 테이블의 전체 데이터를 조회합니다.

![14](/files/images/2019-01-18-Seminar-SQL/14.jpg)

`WHERE` 라는 조건을 추가함으로써 전체 테이블 중에서 조건(Condition)에 맞는 데이터들만 추출합니다.

![15](/files/images/2019-01-18-Seminar-SQL/15.jpg)

단계별로 쿼리를 작성해 보겠습니다.

![16](/files/images/2019-01-18-Seminar-SQL/16.jpg)

매출 데이터가 저장된 테이블이 있다고 가정해 봅시다.

![17](/files/images/2019-01-18-Seminar-SQL/17.jpg)

먼저 특정기간의 전체 매출 상세 내역을 추출하는 과정을 시작합니다.

![18](/files/images/2019-01-18-Seminar-SQL/18.jpg)

`FROM` 절 뒤에는 조회할 테이블의 이름을 작성합니다.

매출 데이터가 존재하는 테이블명을 `FROM` 뒤에 넣습니다.

![19](/files/images/2019-01-18-Seminar-SQL/19.jpg)

`WHERE` 절 뒤에는 날짜 정보를 조건으로 넣습니다.

`created` 라는 Column에는 매출이 발생한 날짜 데이터가 입력되어 있습니다.

특정 기간 내에 발생한 매출 정보만 추출하기 위해서 2018년 12월 1일부터 2018년 12월 31일까지라는 의미의 구문을 조건으로 작성합니다.

![20](/files/images/2019-01-18-Seminar-SQL/20.jpg)

여기에 아이템 ID까지 함께 조건으로 입력하면 특정 기간 내에 발생한 특정 아이템을 구입한 매출 기록을 확인할 수 있습니다.

![21](/files/images/2019-01-18-Seminar-SQL/21.jpg)

추출한 데이터는 마치 스프레드 시트와 비슷한 형식으로 보기 좋게 출력됩니다.

하지만 개수가 많아질 경우 보기가 까다로워집니다.

![22](/files/images/2019-01-18-Seminar-SQL/22.jpg)

만약 전체 매출액을 계산하고 싶다면 어떻게 해야 할까요?

이럴 땐 엑셀의 `SUM` 함수처럼 추출된 데이터(Row)들의 특정 값(Column)의 합계를 구하는 함수가 있습니다.

![23](/files/images/2019-01-18-Seminar-SQL/23.jpg)

엑셀과 마찬가지로 개수를 셀 수 있는 함수도 있습니다.

![24](/files/images/2019-01-18-Seminar-SQL/24.jpg)

특정 기간 뿐만 아니라 특정 아이템에 대한 매출 통계도 구할 수 있지요.

![25](/files/images/2019-01-18-Seminar-SQL/25.jpg)

`WHERE` 절에 조건을 추가하면 특정 기간의 특정 아이템을 판매하여 발생한 총 매출과 매출 건수를 구할 수 있습니다.

![26](/files/images/2019-01-18-Seminar-SQL/26.jpg)

그런데 이런 식이라면 아이템 개수만큼 SQL을 작성해야 합니다.

![27](/files/images/2019-01-18-Seminar-SQL/27.jpg)

`item_id`를 그룹으로 묶어주면 각각의 `item_id`에 대해 쿼리를 수행하여 출력해 줍니다.

이렇게 하면 다른 아이템의 매출 정보를 확인하기 위해 추가로 쿼리를 작성할 필요가 없습니다.

![28](/files/images/2019-01-18-Seminar-SQL/28.jpg)

매출 발생 기간에 대한 조건도 좀 더 직관적으로 변경해 보겠습니다.

![29](/files/images/2019-01-18-Seminar-SQL/29.jpg)

![30](/files/images/2019-01-18-Seminar-SQL/30.jpg)

이외에도 활용할 수 있는 기능들이 엄청 많습니다.

![31](/files/images/2019-01-18-Seminar-SQL/31.jpg)

`JOIN` 이라는 명령어를 통해 연관성있는 데이터끼리 엮어서 데이터를 뽑아낼 수도 있습니다.

![32](/files/images/2019-01-18-Seminar-SQL/32.jpg)

더 많이 알고 싶으시다면 이 웹페이지에서 자세한 내용을 학습하실 수 있습니다.