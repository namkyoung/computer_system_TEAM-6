# 최종보고서
## 1. 문제정의
 매년 동절기마다 독거노인의 사고가 발생하고 있다. 고령화가 점점 증가하는 상황에서 이런 동절기 독거노인의 사고는 사회에 큰 문제로 
대두되고 있다. 동절기 독거노인의 사고가 발생하는 이유는 절약하기 위해서 난방을 충분이 작동시키지 않고 가스의 부족을 제 시간에 
인지하지 못하여 충전이 필요한 시점에 가스 충전을 못하고 있기 때문이다. 그 외에도 난가스와 화재에 노인은 신속한 행동에 취약한 상황이다. 
객관적으로 보건복지가족부에 따르면 노인 85.5%가 복지서비스를 이용하지 못하는 것으로 조사되었다. 이런 상황에서 자동 시스템으로 
독거노인의 사고를 방지해야 한다.
## 2. 해결방안 및 유사사례
###1) 해결방안
중앙 관리 자동화 시스템을 구축하여 그 기능으로 가스 누출/화재 감지, 119 자동신고, 가스업체 자동신고, 
자동난방으로하여 동절기 독거노인 사고를 해결할 수 있다.
###2) 유사사례
![유사사례](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%9C%A0%EC%82%AC%EC%82%AC%EB%A1%80.jpg?raw=true)        
해당 시스템은 화재 상황을 감지하는 연기를 감지하여 독거노인과 같은 현 상황에 대한 상황 파악이 느려 자칫 큰 사고로 
이어질 수 있는 수혜자에게 무선통신이 가능한 Gate Way를 설치하여 사고정보를 취득, 음성녹음 형태로 현 상황 정보를
119에 자동적으로 신고하여 119에서는 위험도를 파악하여 상황에 따른 즉각적인 조취를 취한다.
## 3. 시스템 설계
### 1) 시스템 목적
센서 모듈을 이용해 독거노인들의 동절기 사고 방지와 복지 서비스를 개선에 목적을 둔다.
###2) 시스템 구조
#### ⓵ 전체 시스템 구조
![전체시스템구조](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%A0%84%EC%B2%B4%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B5%AC%EC%A1%B0.jpg?raw=true)
####⓶ 서버 구조
![서버구조](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%84%9C%EB%B2%84%EA%B5%AC%EC%A1%B0.jpg?raw=true)
###3) 시스템 기능
![시스템기능](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B8%B0%EB%8A%A5.jpg?raw=true)
###4) 시스템 구성요소
####- 구성 요소1 - 서버
 ⓵ 기능: 각종 수치를 각 기준에 맞추어 계산
          1) 가스농도 초과시 - 알람 신호 전송 및 소방본부에 신고
          2) 화재감지 검출시 - 알람 신호 전송 및 소방본부에 신고
          3) 가스부족 감지시 - 가스업체에 연락
  ⓶ 입력 데이터: 통신모듈로부터 얻은 각종 수치
  ⓷ 출력 데이터: 알람 시그널, 소방본부 신고 시그널, 가스업체 연락 시그널
####   - 구성 요소2 - 가연성 가스감지 모듈
  ⓵ 기능: 대기 중 가연성 가스량 수집 및 수치화ㅏ
  ⓶ 입력 데이터: 가스 농도 데이터
  ⓷ 출력 데이터: 가스 농도 수치

####  - 구성 요소3 - 화재 감지 모듈
  ⓵ 기능: 주변 환경 데이터(불꽃 감지 센서, CO2센서, 온도센서, 습도센서) 수집 및 수치화
  ⓶ 입력 데이터: 화재 발생으로 인한 주변 환경 변화 데이터
  ⓷ 출력 데이터: 화재 발생에 따른 상승하는 수치(현재 온도, 떨어지는 습도, 증가하는                         CO2, 불꽃 감지)     

####  - 구성 요소4 - 가스 잔여량 표시 모듈
  ⓵ 기능: 가스 잔여량을 수집 및 수치화, 디스플레이
  ⓶ 입력 데이터: 가스 잔여량 데이터
  ⓷ 출력 데이터: 가스 잔여량 수치

####  - 구성 요소5 - 통신 모듈
  ⓵ 기능: Zigbee를 통해 수치들을 수집하여 서버로 전송
  ⓶ 입력 데이터: 각각의 다른 센서모듈에서 수집된 수치
  ⓷ 출력 데이터: 수집된 수치를 서버로 전송

####  - 구성 요소6 - 자동난방 모듈
  ⓵ 기능: 실내적정온도미만 시 자동 난방 -> 적정온도 유지
  ⓶ 입력 데이터: 현재 온도
  ⓷ 출력 데이터: 적정 온도보다 낮다면 보일러 모듈을 ON시키는 시그널 전송
####  - 구성 요소7 - 알람 모듈
  ⓵ 기능: 알람 발생
  ⓶ 입력 데이터: 알람 신호 시그널
  ⓷ 출력 데이터: 알람 발생 ON 시그널
###4) 시스템 동작흐름
####시스템 기능1 - 가스 누출 감지 및 경고 발생
![시스템기능1](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B8%B0%EB%8A%A51.jpg?raw=true)
####시스템 기능2 - 화재 감지 모듈
![시스템기능2](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B8%B0%EB%8A%A52.jpg?raw=true)
####시스템 기능3 - 통신망
![시스템기능3](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B8%B0%EB%8A%A53.jpg?raw=true)
####시스템 기능4 - 가스 잔여량 표시 모듈
![시스템기능4](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B8%B0%EB%8A%A54.jpg?raw=true)
####시스템 기능5 - 자동 난방 모듈
![시스템기능5](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B8%B0%EB%8A%A55.jpg?raw=true)
####시스템 기능6 - 알람 모듈
![시스템기능6](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EC%8B%9C%EC%8A%A4%ED%85%9C%EA%B8%B0%EB%8A%A56.jpg?raw=true)

## 4. 핵심 컴포넌트 상세설계
## 5. 실험 평가
###1) 실험 및 평가의 목적  
 ⓵ 실험 결과로 무엇을 보여줄것인가 ? : 가스 남은량과 화재를 감지할 수 있고, 자동으로 화재신고 및 주유서비스가 가능하다.  
 ⓶실험 결과로 무엇을 주장할것인가 ? : 동절기 취약지구인 독거노인가구에 이 시스템이 필요하다.  
    
###2) 실험 종류  
 시스템 스터디 : 시스템의 기술적인 특징이나 기능 측면  
    
##3) 실험 방법  
- 실험 종류 : 시스템 스터디  
    - 시뮬레이션 환경에서 성능 측정  
    - 시뮬레이션 환경 : 하나의 모형 집에서 각각의 상황에 따른 시스템 동작 확인  
    - 중요지표 : 가스 감지 및 화재감지의 정확성  
  
###4) 평가 지표  
 ⓵ 가스 농도 기준치에 도달 했을 시 알람이 작동하는가?  
  - 독립변수 : 프로판 가스, 일산화탄소 농도  
  - 종속변수 : 서버에서의 가스농도 감지 시간, 가스누출지역 알람시간, 가스검출 에러율  
  - 가스 농도는 1ppm 씩 증가시킨다. (ex 1ppm, 2ppm, 3ppm)  
    1) 프로판 가스만 넣는다.  
    2) 일산화탄소만 넣는다.  
    3) 프로판 가스와 일산화탄소를 동시에 넣는다.  
  
⓶ 화재 발생 시 알람이 작동하는가?
  - 독립변수 : 온도, 습도, 이산화탄소 농도  
  - 종속변수 : 서버에서의 화재감지시간, 화재지역 알람 시간, 화재감지 에러율  
  - 온도, 습도, 이산화탄소의 양을 측정한다.  
    1) 온도, 습도, 이산화탄소의 양을 직접 조절하여 알람이 작동하는 지 확인한다.  
    2) 모형에 화재를 발생시켜 각각의 지표를 측정하여 알람이 작동하는지 확인한다.  
  
⓷ 위 두가지(1,2) 상황 발생 시 119에 신고가 되는가?
  - 119신고 시 해당 거주자에게 문자 발송  
  - 서버에 119신고 기록 저장  
  
⓸ 가스 남은 양이 확인이 되는가
  - 가스 통에 가스를 0.5L 씩 줄인다.(ex 10L, 9.5L, 9L ~ 3L)  
  - 3L 이하로 측정될 시 알람이 작동한다.  
  
⓹ 가스업체에 연락이 되는가
  - 문자와 메일 전송  
  - 서버에 가스 충전 여부를 기록한다.  
  
⓺ 데이터가 신뢰성있게 전송되는가
  - 독립변수 : 데이터 패킷 사이즈, 데이터 전송 주기  
  - 종속변수 : 데이터 전송 신뢰도, 데이터 전송 지연시간  
     1) 데이터의 패킷 사이즈를 조절하여 데이터의 누락 여부와 전송 지연시간을 검출한다.  
     2) 데이터 전송 주기를 조절하여 데이터의 누락 여부와 전송 지연시간을 검출한다.  
    
###5) 결과 분석, 해석 방법  
- 가스 농도 기준치 검사 측정 결과의 정확성  
- 화재 감지 검사 정확성  
- 119 신고 및 신고 시간의 정확성  
- 가스 남은 양 검출의 정확성  
- 데이터 전송 신뢰성  







## 6. 개발 환경 및 구현에 필요한 기술
###1) 개발 환경
![개발환경](https://github.com/namkyoung/computer_system_TEAM-6/blob/master/Images/%EA%B0%9C%EB%B0%9C%ED%99%98%EA%B2%BD.jpg?raw=true)
## 7. 개발 환경에 대한 조사
## 8. 마무리