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
- 위 그래프와 마찬가지로 강남구, 용산구, 마포구가 진하게 표시된 것을 확인할 수 있고 서울 외곽일수록 색이 희미해는 것을 볼 수 있다.

![image](https://user-images.githubusercontent.com/75618206/203449254-20326955-8d4b-4810-9ab8-933469975343.png)
- 카페디저트가 가장 많은 수를 차지하고 있다.

![image](https://user-images.githubusercontent.com/75618206/203449318-3875876b-d392-4c8f-9a51-ff85943cdc0f.png)
- 만원 미만의 맛집이 가장 많고 가격대가 올라갈수록 맛집의 개수가 줄어드는 경향을 확인할 수 있다. 
- 가격대별 평균 평점 그래프를 통해 가격대가 높아질수록 평점이 높은 것을 확인했지만, 가격대가 올라갈수록 맛집의 개수는 줄어든다.

![image](https://user-images.githubusercontent.com/75618206/203449750-55c48bfa-d2e2-45a0-9348-05f3244e1cf4.png)
- 지오코드 : 주소를 이용하여 위경도 좌표를 반환하는 메소드
- 지오코드를 이용하여 맛집의 주소를 위경도 좌표로 변환했고 포리움 맵을 활용해서 지도에 마커를 생성해 맛집의 분포를 표현.
- 마커에 지역, 상호명, 평점, 음식분류, 가격대를 보기 쉽게 나타냈다.

### 3-5. 인구와 맛집 상관관계
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

## 프로젝트 결과
[데이터 시각화 Viewer Link](https://nbviewer.org/github/cyless-hj/Restaurant-Data-Visualization-PJT/blob/master/%EB%8D%B0%EC%9D%B4%ED%84%B0%20%EC%8B%9C%EA%B0%81%ED%99%94%20%EC%B5%9C%EC%A2%85%EB%B3%B8.ipynb)
