# 닥터 솔저(Doctor Soldier)

닥터 솔저는 군인들에게 **'전문가가 자신을 관리해준다.'**는 느낌을 주게 하는 모바일용 웹앱 (Single Page Application)입니다.

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

 Node.js를 처음 보고, Web에 쓰이는 JavaScript로 서버를 만들 수 있다는 신선함처럼, 저에게 Vue.js는 Web을 만들 줄 안다면, 이제는 서버뿐만 아니라 모바일 애플리케이션까지 만들 수 있다는 신선한 충격을 주었습니다.

 서버에서부터, 모바일까지 이제 Web은 정말 실용성 있는 분야라고 생각됩니다. 이러한 영감을 받아, 저는 실용성에 초점을 두어 필요한 기능들을 **한곳에 모아 둔,** **군인을 위한, 실용성** **있는** **모바일 용 웹 앱**을 만들기로 결심했습니다.

![](https://drive.google.com/open?id=1Yd7COLkMqmge8qwCGVw8R7QXqpVeXhEe)

 닥터 솔저는, 군인들에게 마치 **전문가가 자신을 관리**해준다는 느낌을 주는 앱이며 실용성 있는 다양한 서비스로 **장병들에게 널리 사용될 애플리케이션**이 될 것입니다. 차후, 국방부 관련 이벤트 푸시 메세지를 하는 등 **다양한 서비스를 창출**할 수 있을 것입니다.

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

### 스크린샷

------

[](https://drive.google.com/open?id=1Yd7COLkMqmge8qwCGVw8R7QXqpVeXhEe)

[](https://drive.google.com/open?id=1zasVr3BC-pKyB2vYSFwJzuHGwRjU-Cp7)

[](https://drive.google.com/open?id=1sPzmfdIqgbHiqCWFyimUtM7T6pYWZCUw)

[](https://drive.google.com/open?id=1Ah4iDEmjqidhBuz4IfCZBegeWk1DvffD)

[](https://drive.google.com/open?id=1k9-WkKefIXqJaX-PLCu9gTbjGhzJkBze)

[](https://drive.google.com/open?id=1QyJKXk_mm9FaFaGlPpNS63boY9ty-Dt4)

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

추가바람

#### 저작권 및 사용권 정보 (Copyright / End User License)

- MIT

#### 배포자 및 개발자의 연락처 정보 (Contact Information)

- leedh2008@naver.com

#### 알려진 버그 (Known Issues)

- javaScript 부동소수점으로 인한 약간의 계산 오차

#### 문제 발생에 대한 해결책 (Troubleshooting)

- Big Decimal 라이브러리 사용예정

#### 크레딧 (Credit)

- 추가바람

#### 업데이트 정보 (Change Log)

- 191024 0.0.1