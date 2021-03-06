# 2021 공공빅데이터 분석 공모전🚚

![배너2](https://user-images.githubusercontent.com/77844152/136762796-dddfbee3-d27b-4c8c-a25c-c0a39d14e66b.PNG)
(2021.09.06~2021.10.11)


## 목차
- [프로젝트 목표](#프로젝트-목표)
- [데이터 목록](#데이터-목록)
- [전처리 과정](#전처리-과정)
- [군집 분석](#군집-분석)
- [최종 시각화](#최종-시각화)
- [프로젝트 보고서](#프로젝트-보고서)
- [Contributors](#Contributors)

## 프로젝트 목표

현 택배 시스템의 개선을 위해 무인 택배함의 공급을 늘리고 이를 위한 우선 설치 입지 선정하는 것이 본 프로젝트의 목적이다. 전국적인 무인 택배함의 공급을 위해 우선적으로 서울시에서 무인 택배함을 보급하는 계획을 세웠다. 따라서 무인 택배함 우선 입지 선정 시 기준이 되는 변인을 추출하고 서울시 행정동별 변인 분포를 살펴본다. 그리고 우선적으로 무인 택배함을 설치할 행정동과 입지를 선정한다.

## 데이터 목록

| **데이터명**                           | **연도** | **출처**                                         |
| -------------------------------------- | -------- | ------------------------------------------------ |
| 서울시 가구원수별   가구수 (동별) 통계 | 2020     | 서울시 열린데이터 광장                           |
| 서울시  주택종류별 주택 (동별) 통계    | 2020     | 서울시  열린데이터 광장                          |
| 여성  안심 택배함 위치                 | 2021     | https://news.seoul.go.kr/welfare/archives/511589 |
| Box25  위치                            | 2021     | https://map.gspostbox.com/box25/                 |
| 서울시 우편물 취급 (구별)  통계        | 2021     | 서울시 열린데이터 광장                           |
| 서울시 소비 활동 지수                  | 2020     | 서울특별시 빅데이터 캠퍼스                       |
| 서울시 인구밀도 통계                   | 2021     | 서울시 열린데이터  광장                          |
| 서울시 블록단위 지역 경계도            | 2019     | 서울특별시 빅데이터 캠퍼스                       |
| 서울시 행정동 경계데이터               | 2020     | https://github.com/vuski/admdongkor              |

데이터 용량이 커서 업로드 할 수 없어 최종 scaling한 csv만 업로드함.  
서울특별시의 행정동은 2020년 1월 변경사항까지 고려함.  

## 전처리 과정

- 변인 1 : 1인가구 비율이 높을 수록 무인택배함의 사용률이 높음. 따라서 행정동별 **1인가구 비율**을 정제.
- 변인 2 : 다가구주택/연립주택/단독주택에서 택배 배송이 어려움. 따라서 앞선 **주택들의 배송난이도**에 따라 가중치를 부여해 행정동별 가중합을 구해줌.
- 변인 3 : 무인택배함이 부족한 지역에 우선설치가 필요함. 따라서 기존의 여성안심택배함과 Box25의 행정동별 공급량을 고려하여 행정동별 **무인택배함의 개수**를 추출
- 변인 4 : 택배를 많이 받는 지역에 무인택배함이 우선적으로 설치되어야함. 따라서 우편물 취급통계와 홍쇼핑 결제건수를 이용하여 행정동별 **택배 물동 예측량**을 추출
  
전처리 완료된 4가지의 변인값들을 0~1사이의 값으로 scaling 해주었다.(min-max scaling)

## 군집 분석

Elbow method를 사용해 군집의 수를 구하고 아래 3가지 알고리즘으로 군집을 분석함.

- Spectral Clustering
- Gaussian Mixture Clustering
- K-Medoids Clustering  

군집분석 알고리즘 중에서 타겟을 명확하게 추출한 방법을 이용하여 변인들간의 교집합을 구해 최종 입지 행정동을 결정.
## 최종 시각화

최종입지로 선정된 37개의 행정동 중 4가지 변인에서 모두 좋은 점수를 얻은 4개 동을 선정하여 어떤 곳에 우선적으로 무인 택배함을 설치할지 시각화 하고자 한다. 

우선 해당 행정동 거주 시민이 무인 택배함을 많이 이용하기 위해서는, 

**첫번째, 사용자의 안전성**

**두번째, 택배함의 보안성**

**세번째, 거주지와의 접근성**

이렇게 3가지의 조건을 필수적으로 만족해야 한다.

따라서 우리는 유동인구도 많고 주민들이 안전하다고 느낄 수 있는 지하철역, 그리고  관공서에 우선적으로 무인 택배함을 설치하는 것을 목표로 하였다. 관공서 중에서는 국공립 도서관, 경찰서,소방서, 행정복지센터, 시청과 구청, 우체국 등을 우선 설치 지역으로 선정하였다.

시각화 대상동은 **화곡1동,한남동,개봉1동,연희동**이다. 

<img src="https://user-images.githubusercontent.com/77844152/136799385-6d18dd63-f066-4a6f-aa9b-f18d95e604bb.png" width="800" height="400">
<img src="https://user-images.githubusercontent.com/77844152/137274148-6c37a127-3dd8-4372-a37a-bfcabb73f76f.png" width="800" height="400">


## 프로젝트 보고서

Click [Here](https://drive.google.com/file/d/1f1LUHwrMC0ru1HfbPTfhrgSdGw9Nvjw_/view?usp=sharing)



## Contributors

* [김민아](https://github.com/mina-kim-1015)
* [박근아](https://github.com/guen-a-park)
* [이서인](https://github.com/seoin-lee)

