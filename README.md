# 맛집 데이터와 공공데이터를 이용한 서울시 자치구별 맛집 상권분석

팀장 : 김승규
팀원 : 정현진, 김경민, 정서연, 이선희
## 1.	프로젝트 개요

### 1-1. 주제 선정 배경
<p align="center">
<img src = "https://user-images.githubusercontent.com/75618206/203445615-2bdd467f-60dd-49c1-ac2b-c4e28d69b146.png">
</p>

- 서울시는 우리나라에서 면적대비 가장 많은 인구가 살고 있고 그만큼 외식산업의 규모가 매우 크다.
- 식당 창업에 뛰어드는 기업과 소상공인이 점점 증가하고 있는데, 포화된 산업인 만큼 창업을 계획할땐 데이터를 기반하여 창업할 위치,음식종류,음식의 가격대 등 많은 부분을 고려하고 신중히 결정해야할 필요가 있다.

### 1-2. 프로젝트 목표
1. 서울시 다양한 공공데이터 활용 및 크롤링을 통한 맛집데이터 수집
2. 맛집 데이터와 공공데이터 간의 다양한 상관관계 분석
3. 서울시 맛집 상권분석에 필요한 다양한 인사이트 도출 및 창업 아이디어 제안

### 1-3. 기술 스택
- 데이터 전처리 및 시각화 : <img src="https://img.shields.io/badge/Jupyter-F37626?style=flat-square&logo=Jupyter&logoColor=white">
- 웹 크롤링 : <img src="https://img.shields.io/badge/Selenium-43B02A?style=flat-square&logo=Selenium&logoColor=white">

## 2. 데이터 프로세싱

### 2-1. 데이터 수집
- 서울 열린데이터 광장 공공 데이터 활용
- 이용 데이터 List
  1. 서울시 자치구 별 인구수
  2. 서울시 자치구 별 소득세
  3. 서울시 자치구 별 GDP 
  4. 서울시 자치구 별 사업체 수
  5. 서울시 자치구 별 사업체 종사자 수
  6. 서울시 소재 지하철역 주소
  7. 서울시 소재 대학교 주소

### 2-2. 웹 크롤링
- 맛집 데이터를 얻기 위해 크롤링 할 웹사이트 '망고 플레이트' 선정
- Selenium을 이용해 구 별 맛집 데이터 동적 크롤링
- 데이터 정제
  - 불필요한 반복문자 삭제
  - 예외처리를 통해 null 값 처리
  - 데이터 병합

<p align="center">
<img src = "https://user-images.githubusercontent.com/75618206/203446962-caaf7656-57cd-4220-8b63-2e446377ce00.png">
<img src = "https://user-images.githubusercontent.com/75618206/203447098-0a02934f-6a2f-4bb7-9b84-62c79dc20f53.png">
</p>

## 3. 데이터 시각화

### 3-1. 카테고리
1. 기본 시각화
2. 인구
3. 활동인구 / 사업체/ 인프라
4. 소득(GDP)

### 3-2. 맛집 선정
<p align="center">
<img src = "https://user-images.githubusercontent.com/75618206/203447864-a66c8888-bf39-4bf7-b347-9d016e797fab.png">
</p>

- 각 가격대의 맛 평가 비율을 파이차트 Subplot으로 한눈에 표현해 보았을 때, 맛있다, 괜찮다, 별로다 수의 비율이 비슷하고 모든 가격대에서 90%에 가까운 비율이 맛있다라고 평가했다.
- 따라서 이대로 데이터를 활용할 수 없다고 판단, 가중치를 적용하여 새로운 평점 산출
  - (별점 * 맛있다 수 - 2 * 별점 * 별로다 수) / 전체 리뷰수
- 이렇게 산출된 평점을 적용해 3.5이상의 평점을 받은 식당을 자체적으로 맛집으로 선정.

<p align="center">
<img src = "https://user-images.githubusercontent.com/75618206/203448199-422de7e6-c1c6-4e6f-a73b-bd0b51226b39.png">
</p>

### 3-3. 가격대 별 평균 평점
<p align="center">
<img src = "https://user-images.githubusercontent.com/75618206/203448637-be9c2b06-55cb-4399-beed-2c822c2c493a.png">
</p>

- 가격대별 맛집 평균점수를 바차트로 표현
- 가격대가 높아질수록 맛집 평균점수도 비례하여 높아지는 것을 볼 수 있다.
- 가격대가 높을수록 사람들은 음식이 맛있다고 느끼는 경향이 있는 것으로 보인다.

### 3-4. 가격 점수 도출
- 가격대는 범위값, 가격대에 대한 분석을 진행하고자 가격점수라는 상대값을 생성
- 10000원 미만에 1점 20000만원 미안에 2점 40000원 이상에 5점을 부여하여 해당되는 구별 맛집수를 곱한 후 구의 전체 맛집수로 나누어 산정
![image](https://user-images.githubusercontent.com/75618206/203448956-32217035-e693-41ee-afef-e69b46151b55.png)
- 강남구의 맛집 가격대가 가장 높고 강북구가 가장 낮은 것으로 보인다.

### 3-5. 기본 시각화
![image](https://user-images.githubusercontent.com/75618206/203449150-ac22526b-baf7-4e36-992f-b99e85a0681e.png)
- 강남구, 마포구, 용산구 순으로 맛집의 수가 많이 분포하고 있다.

![image](https://user-images.githubusercontent.com/75618206/203449992-9a7c477b-ff81-4473-859d-ba351d4a0afb.png)
- 위 그래프와 마찬가지로 강남구, 용산구, 마포구가 진하게 표시된 것을 확인할 수 있고 서울 외곽일수록 색이 희미해지는 것을 볼 수 있다.

![image](https://user-images.githubusercontent.com/75618206/203449254-20326955-8d4b-4810-9ab8-933469975343.png)
- 카페디저트가 가장 많은 수를 차지하고 있다.

![image](https://user-images.githubusercontent.com/75618206/203449318-3875876b-d392-4c8f-9a51-ff85943cdc0f.png)
- 만원 미만의 맛집이 가장 많고 가격대가 올라갈수록 맛집의 개수가 줄어드는 경향을 확인할 수 있다. 
- 가격대별 평균 평점 그래프를 통해 가격대가 높아질수록 평점이 높은 것을 확인했지만, 가격대가 올라갈수록 맛집의 개수는 줄어든다.

![image](https://user-images.githubusercontent.com/75618206/203449750-55c48bfa-d2e2-45a0-9348-05f3244e1cf4.png)
- 지오코드 : 주소를 이용하여 위경도 좌표를 반환하는 메소드
- 지오코드를 이용하여 맛집의 주소를 위경도 좌표로 변환했고 Folium 맵을 활용해서 지도에 마커를 생성해 맛집의 분포를 표현.
- 마커에 지역, 상호명, 평점, 음식분류, 가격대를 보기 쉽게 나타냈다.

### 3-6. 인구와 맛집 상관관계
![image](https://user-images.githubusercontent.com/75618206/203450395-651eb51e-dba3-418c-b3d5-3408269ca52d.png)
- 인구와 맛집 수를 산점도로 표현
  - X축 : 맛집 수
  - Y축 : 인구 수
- 인구 수가 많다고 맛집 수가 많은 것은 아니다.

![image](https://user-images.githubusercontent.com/75618206/203450530-15d50b79-1de5-41c9-a218-6a16da98d36f.png)
- Seaborn 패키지 regplot
  - 산점도와 선형회귀분석에 의한 회귀선을 함께 나타낸다.
    - X축 : 총 인구수
    - Y축 : 리뷰수
- 구 별 인구 수와 리뷰 수는 서로 상관관계가 없다고 볼 수 있다.

### 3-7. 맛집과 활동인구 / 사업체 / 인프라 상관관계
![image](https://user-images.githubusercontent.com/75618206/203451172-10dd4cd7-3393-416e-9ca2-98505f3fe62d.png)
- 상관계수의 성질
  - 상관계수의 값은 -1과 1사이의 범위에 있다.
  - X와 Y사이에 상관이 없으면 상관계수 값은 0이다.
  - 연구의 성격과 자료의 특성에 따라 다르나, 대체적으로 0.3 이상이면 상관관계가 존재한다고 평가
- 맛집수와 사업체종사자수는 강한 상관관계를 가지고 있다.
  - 사업체 종사자 수가 적을수록 맛집 수 또한 적다.

![image](https://user-images.githubusercontent.com/75618206/203451390-30cdff9d-7029-4def-9ac5-751235e7bb47.png)
- 맛집 수와 사업체 수는 꽤 큰 상관관계를  가지고 있다.
  - 보통 사업체 수가 많은 곳에 맛집도 많이 분포한다.

- 맛집 수에 영향을 미치는 요소로 주거 인구 수 보다 일하고 있는 사람의 수 즉, 활동 인구 수가 더 중요하다는 결과를 도출할 수 있었다.

![image](https://user-images.githubusercontent.com/75618206/203451484-05877752-4b1b-44b3-b4d9-72d3d4210b64.png)
- Haversine : 둥근 지구표면에 있는 두 좌표 사이의 거리를 구하는 방법
- 왼쪽의 인접 대학교에서의 거리에 따른 맛집 수 그래프를 보면 0.5~1km 사이에 맛집이 가장 많이 위치한 것을 볼 수 있다.
- 간단히 생각해 봤을 때 대학교에 가까울수록 맛집의 수가 많을 것이라고 생각했으나 예상 외로 반경 500m에서 1km 사이에 가장 많이 위치한 것을 볼 수 있다.
- 쪽은 인접 지하철역에서의 거리에 따른 맛집 수 그래프이다.
- 간단히 예상되는 결과와 같이 지하철역에 가까울수록 맛집의 수가 많은 모습을 볼 수 있다.

### 3-8. 소득(GDP)과 맛집의 상관관계
![image](https://user-images.githubusercontent.com/75618206/203452174-33b4d10e-5fe6-4461-bf24-9f4e2577a6b6.png)
- GDP가 낮은 쪽이 가격점수도 낮은 걸로 나타나므로 둘은 강한 상관관계를 가진다.
  - 총생산이 높을수록 맛집 평균 가격대가 올라간다.

![image](https://user-images.githubusercontent.com/75618206/203452267-df426564-536a-4e93-b6a3-ac4e90d507e2.png)
- 소득세를 많이 내는 구 일수록 맛집의 수가 많은 경향을 보여준다.

![image](https://user-images.githubusercontent.com/75618206/203452377-2987d873-4e25-46b4-a451-fea1dfd45748.png)
- 위에서 정의한 맛집이 아닌 전체 음식점에 대하여 시각화한 그래프.
- 소득세를 많이 내는 구 일수록 음식점의 가격점수가 높은 경향을 보여준다.
- 이 자료들을 통해 GDP와 소득세에 따라 가격점수가 올라가는 즉, 소득이 높을수록 가격대가 높아지는 경향을 확인 할 수 있다.

## 4. 결과 후기 및 기대효과
- 망고플레이트 웹서버가 매우 느린 관계로 첫 리뷰 작성 시점 등의 데이터를 가져오지 못해 아쉬움이 남는다. 
- 그러나 도출된 결과가 요식업 창업에 도움이 될 수 있는 인사이트를 만들었다는 것에 의의를 두었다.
- 데이터 분석과 시각화를 통해 기존에 예상했던 결과가 아닌 의외의 결과를 종종 볼 수 있었는데 이를 통해 평균적인 생각과 실제 형태는 좀 다를 수 있을 수 있다고 느꼈다. 
- 예를 들어 거주인구보다는 활동인구가 맛집 수에 더 많은 영향을 미친다는 것과 같은 분석 결과를 보며 통계 데이터를 통해 보다 현실을 정확히 파악할 수 있는 시각을 얻을 수 있다는 생각을 가지며 프로젝트를 마무리 했다. 
<br>

- 기대효과
  - 다양한 니즈에 따른 정보 확인 가능
    - 식당 창업 시 고려할 정보
    - 가격대 데이터를 통해 음식의 적정가 책정에 도움
    - 가고싶은 맛집의 위치 및 정보
  - 추후 해당 데이터 분석 결과를 바탕으로 경쟁력 있는 음식 종류,가격대 등을 이용하여 맛집 추천 시스템 개발로의 발전 가능성

## 프로젝트 결과 Link
[데이터 시각화 Viewer Link](https://nbviewer.org/github/cyless-hj/Restaurant-Data-Visualization-PJT/blob/master/%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%8B%9C%EA%B0%81%ED%99%94%20%EC%B5%9C%EC%A2%85%EB%B3%B8.ipynb)
