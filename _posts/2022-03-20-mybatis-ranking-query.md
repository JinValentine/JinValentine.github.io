---
layout: single
title: "[MyBatis] 조건검색 랭킹 쿼리문 구현"
categories: MyBatis
tag: mybatis
---

## MyBatis를 이용한 조건검색기능과 리뷰점수 랭킹순 정렬기능 구현

MyBatis를 이용하는 첫 프로젝트에서 쿼리문을 이용한 기능 중 몇 개를 가져와보았다.

**첫번째** 상품코드와 가격, 이름, 상품의 재료를 통하여 취향에 맞는 상품을 찾을 수 있는 조건 쿼리이다.

우선적으로 나는 데이터 결과가 두 테이블이 JOIN을 한 결과가 나와야했기 때문에 resultMap으로 두 테이블을 VO로 묶어서 테이블 결과값을 한번에 나오게했다.

![MenuVo](https://user-images.githubusercontent.com/77107216/159157767-d3c8c55a-0ae2-4e80-bcfb-e12402e6bc10.png)

브랜드, 재료의 경우에는 복수선택이 가능하기에 foreach를 이용하여 입력 값들과 같은 값들을 확인하게 하였다.  
가격은 들어온 값보다 낮은 가격이 결과값으로 나오게 하였다. 마지막으로 메뉴명은 Like문을 이용하여 메뉴명의 부분만 입력되어도 결과값이 나오게 하였다.

![MenuSearch](https://user-images.githubusercontent.com/77107216/159157054-d4b3970d-a0a8-4d31-8b54-91c1bbaca2f4.png)

**두번째** 리뷰를 랭킹순으로 데이터를 추출하는 쿼리문이다.  
이것도 JOIN을 이용하는 쿼리문이기에 이번에는 세 테이블을 묶어두었다.

![RankingVo](https://user-images.githubusercontent.com/77107216/192245680-ec0b93e1-c9c9-4b5c-b3ff-645755942d70.png)

리뷰 승인의 결과를 확인하고 상품에 대한 리뷰의 점수를 평균값을 가져오며 이 평균값을 내림차순으로 정렬한다.
그리고 순위는 10위까지만 필요하기 때문에 ROWNUM을 10까지 주었다.

![ReviewRanking](https://user-images.githubusercontent.com/77107216/192245787-ed503aab-ec7d-4e0f-ac06-50e3999bff3c.png)

**이것을 완성하고 나서 알았지만 JOIN을 위해 Dto테이블을 resultMap에 묶어서 사용을 했지만
이것보다는 <u>HashMap</u>을 이용하면 더 편하게 할 수 있다는 것을 나중에 알게 되었다.**

다음에는 HashMap을 통해서 쿼리문을 작성해 보아야겠다.
