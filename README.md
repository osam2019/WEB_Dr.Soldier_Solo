# 닥터 솔저(Doctor Soldier)

닥터 솔저는 군인들에게 **'전문가가 자신을 관리해준다.'** 는 느낌을 선사하는 모바일용 웹 애플리케이션 (Single Page Application)입니다.

닥터 솔저가 현재 제공하는 서비스는

- 전역일 계산기 (총 일,  한 날, 남은 날, 남은 평일)
- 급여 계산기 ( 월급, 총 급여, 저축, 적금)
- 출타 달력 ( 자신의 출타 달력, 타인의 출타 달력  )
- 건강 ( 몸무게 차트, 비만지수, 칼로리, 현재 체력 등급)
- 기록 ( 군 생활 To-do-List )
- 커뮤니티 기능

과 같은 서비스 등이 있고, 향후 서버가 생기면 API를 이용해 군인들을 위한 더 많은 서비스를 제공할 예정입니다!

### 현황

------

- 2019 국방부 오픈소스 아카데미 공개 SW 집체교육 WEB 분야 산출물 (데모) 

- 28사단 포병연대 268포병 대대 병장 이도현
- 개발기간 : '19 10 21 ~ '19 10 25

### 개발 배경 

------

 SPA(Single Page Application)이라는 단어를 오픈소스 아카데미를 통해 처음으로 접했습니다. SPA를 보자마자 '이거 모바일 앱 아니야?'라는 생각이 들었습니다. 

 Node.js를 처음 보고, Web에 쓰이는 JavaScript로 서버를 만들 수 있다는 신선함처럼, 저에게 Vue.js의 SPA는 Web을 만들 줄 안다면, 이제는 서버뿐만 아니라 모바일 애플리케이션까지 만들 수 있다는 신선한 충격을 주었습니다.

 서버에서부터, 모바일까지 이제 Web은 정말 실용성 있는 분야라고 생각됩니다. 이러한 영감을 받아, 저는 실용성에 초점을 두어 필요한 기능들을 **한곳에 모아 둔,** **군인을 위한, 실용성** **있는** **모바일 용 웹 앱**을 만들기로 결심했습니다.

![](https://drive.google.com/uc?export=view&id=1Vr-g32liMfnXJkwY6El8Nw8Z6QVaFbI2)

 닥터 솔저는, 군인들에게 마치 **전문가가 자신을 관리**해준다는 느낌을 주는 서비스이며 실용성 있는 다양한 서비스로 **장병들에게 널리 사용될 애플리케이션**이 될 것입니다. 그렇게 된다면, 국방부 관련 이벤트 푸시 메세지를 하는 등, 군인들의 편의를 위한 **다양한 서비스를 제공** 또는 군인을 대상으로 한 광고 등으로 수익을 창출 할  수 있을 것입니다.

### 개발 문서

------

###### 초기 구상

![](https://drive.google.com/uc?export=view&id=13-GIM4JdxTwkWZvDF5zbYBF2Uoxte-N9)

(~~개발문서를 공개할 줄 몰랐습니다.~~.)

###### 초기 목표

 군인들에게 경제, 헬스, 생활 면으로 다양한 정보를 제공하고, 솔루션을 제공하는 웹 어플리케이션 개발

- 군생활 계산기
- 군생활 목표 To-do-list
- 휴가 달력
- 몸무게 차트
- 체력 등급표
- 적금 계산기

------

###### 기술 스택

Vue.js, jquery

Element ui, ApexChart, Font awesome, Google Fonts

node.js & express.js (예정)

mongoDB (mongoose): NoSQL 데이터베이스(예정)

------

###### 백 엔드 ( 예정 )

- RESTful API
- Passport를 이용한 Facebook, Google, Naver, KaKao 로그인
- Image 파일 압축 후 저장
- compression 미들웨어 
- helmet 미들웨어

###### 프론트 엔드

- 애니메이션 : Velocity, animate(jQuery)
- ApexChart를 이용한 리얼타임 차트제공
- axios를 통한 API 접근(예정)
- Vuex 사용(예정)
- vue-router 사용(예정 / Community 서비스에 이용 ) 

###### 참고 자료

-  BMR(basal metabolic rate) Calculate :  Mifflin St Jeor Equation(채택), harris-benedict equation
- BMI 계산법, BMI 기준, 소화흡수열량 공식
- 월적금 복리, 단리 계산법

### 향후 계획

------

###### 1. 프로젝트 관련

- 커뮤니티 서비스 프론트엔드 완성
- 로그인 서비스 프론트엔드 완성
- 프론트엔드 디자인 개선
- 서버 생성(Node.js)

###### 2. 서비스 관련

- BigDecimal 라이브러리를 이용한 보다 정확한 계산 구현
- 커뮤니티 서비스 완성
- 국방부 관련 이벤트 모음 페이지 개발

### 정보

------

#### 컴퓨터 구성 / 필수 조건 안내(Prerequisites)

- Node.js
- Recommend Chrome

#### 설치 안내(Installation Process)

- project clone
- npm install

#### 사용법(Getting Started)

- npm run dev
- http://localhost:8080 접속

#### 파일 정보 및 목록(File Manifest)

추가예정

#### 저작권 및 사용권 정보 (Copyright / End User License)

- MIT License

#### 배포자 및 개발자의 연락처 정보 (Contact Information)

- leedh2008@naver.com

#### 알려진 버그 (Known Issues)

- javaScript 부동소수점으로 인한 약간의 계산 오차

#### 문제 발생에 대한 해결책 (Troubleshooting)

- Big Decimal 라이브러리 사용예정

#### 크레딧 (Credit)

- 추가예정

#### 업데이트 정보 (Change Log)

- 191024 0.0.1



### 스크린샷

------

![](https://drive.google.com/uc?export=view&id=1Vr-g32liMfnXJkwY6El8Nw8Z6QVaFbI2)

![](https://drive.google.com/uc?export=view&id=1y0lET6vWDbhbhSSO113-1NNXE6zq3YQs)

![](https://drive.google.com/uc?export=view&id=13wISoIWEPvwOo0qO5B--11IJ6DpCX4YI)

![](https://drive.google.com/uc?export=view&id=1-rRgFSU1r6ybRbThImnEHoqIEvw91Esa)

![](https://drive.google.com/uc?export=view&id=1h-UDCJDJRsUcbgicTfq5JHZzKXOc0td9)

![](https://drive.google.com/uc?export=view&id=1htqECALPFgUk4LEQ9JQ195nRpoCnvYdt)

![](https://drive.google.com/uc?export=view&id=1V1Mf8ILLw3ZTwD-DvLhjveOXqLZpg1HF)
