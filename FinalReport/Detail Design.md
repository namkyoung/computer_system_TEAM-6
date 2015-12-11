
컴시설 - 상세 설계 보고서
===================


본 보고서는 상세 설계에 관한 보고서입니다. 해당 상세 설계의 내용은 본 프로젝트의 핵심인 서버의 클래스들을 중심으로 작성하였으며, 각각의 기능에 대한 세부 보고서 입니다.

--------------------


Documents
-------------

다음은 서버에서 구현될 클래스들의 목록입니다.

> **Server:**

> 1. **집 개별 정보 클래스**
> 2. **가스 농도 감지 클래스**
	> -함수1: 대기 중의 가스 농도 기준치 검사 함수
	> -함수1: 대기 중의 가스 농도 기준치 검사 함수
> 3. **화재 감지 클래스**
	> -함수1: 주변 환경 기준치 검사
> 4. **가스 부족 감지 클래스**
	> -함수1: 가스 잔존량 기준치 검사
	> -함수2: 가스 업제 공급 요청 접수
> 5. **자동 난방 클래스**
	> -함수1: 상속받은 현재 온도 데이터에 따른 난방 여부 기능
	> -함수2: 현재 온도에 따른 보일러 on/off 함수
> 6. **위험 알람 함수**



### 시스템 구현 핵심 요소 클래스


#### <i class="icon-file"></i> **1. 집 개별 정보 클래스**

_각각의 독거노인 거주지를 기반으로 분배하기 위한 가장 기본이 되는 클래스_

```
// House Class
Class House
{
	int  H_Number  // 집 번호
	char H_Address  // 집 주소
	char P_Number  // 연락처

	GetH_Address()
	SetH_Address()
	GetP_Number()
	SetP_Number()
}
```

#### <i class="icon-file"></i> **2. 가스 농도 감지 클래스**

_공기 중의 가스 농도를 감지하기 위한 클래스로서 총 3가지의 기능을 갖는다._

> 180초마다 계산 -> 정부기관에서 각종 기준치 조사 -> 119자동신고, 위험상황알람

```
// Gas_Concentration Class
Class Gas_Concentration
{
	int H_Number	   // 집 번호
	double P_convalue   // 프로판가스 농도
	double CO_convalue // 일산화탄소 농도
}

// 함수1: 대기 중의 가스 농도 기준치 검사 함수
Gas_ConThresholds()
{ 
	while(else Repeated every 180 seconds) {
		if P_convalue > 5ppm or  CO_convalue > 10ppm then
			alarm = 1
	}
}
```


#### <i class="icon-file"></i> **3. 화재 감지 클래스**

_화재를 감지하기 위한 클래스로서 총 3가지의 요소 데이터를 취득한다._

> 1) 온도
> 2) CO2
> 3)습도
> 1, 2, 3의 데이터를 통해 일정시간동안 변화량으로 화재를 감지
> 180초마다 계산 -> 119자동신고, 위험상황알람

```
// Fire_sensing Class extends House Class
Class Fire_Sensing extends House Class
{
	int H_number	        // 상속받은 House 클래스의 집 번호
	double T_value1      // 이전 온도
	double T_value2	 // 현재 온도
	double CO_value1    // 이전 이산화탄소 농도
	double CO_value2    // 현재 이산화탄소 농도
	double H_value1     // 이전 습도
	double H_value2     // 현재 습도
}

// 함수1: 주변 환경 기준치 검사
Sur_Environment()		// 주변 환경 기준치 검사 함수
{ 
	while (Repeated every 180 seconds) {
		if (T_value2 - T_value1) > 10℃  
		or (CO_value2 - CO_value1) > 100ppm 
	      	or H_value2 - H_value1 < 10% then
			alarm = 1, report = 1 // 비상 알림 및 업체 보고
		else T_value1 = T_value2 
		    CO_value1 = CO_value2 
		    H_value1 = H_value2 	          
	}
}
```


#### <i class="icon-file"></i> **4. 가스 부족 감지 클래스**

_가스 통을 매일 체크하며 가스가 일정량 이하로 남아있을 경우 자동으로 보고한다._

> 하루 3번 계산 -> 가스업체 알림

```
// Gas_Storage Class
Class Gas_Storage extends House class
{
	int H_number	        // 상속받은 House 클래스의 집 번호
	int Term_time
	int Gas_stovalue
}

// 함수1: 가스 잔존량 기준치 검사
Gas_Remaining()
{
	while(Repeated every 6 hours) {
		if Gas_stovalue < 3liter then
			request = 1
	}
}

// 함수2: 가스 업제 공급 요청 접수
RequestGas() : House 클래스 상속
{
	if request = 1 then ring GasEnterprise 
	{
		House.GetH_Address()
		House.GetP_Number()
	}
}
```



#### <i class="icon-file"></i> **5. 자동 난방 클래스**

_자동적으로 집 안 내의 온도를 조절하기 위한 기능으로 화재 감지 클래스의 데이터에서 받아온 현재 온도 데이터를 기반으로 하여 난방기 작동 여부를 결정한다._

> 1) 화재감지검출 모듈로부터 상속받은 온도
> 2) 보일러 on/off

```
// Auto_Temper_Stable Class
Class Auto_Temper_Stable extends Fire_Sensing Class
{
	double T_value2	 // 화재 감지 클래스에서 상속받은 현재 온도
	int warm_on_off
}

// 함수1: 상속받은 현재 온도 데이터에 따른 난방 여부 기능
AutoTemp()
{
	while(Repeated every 180 seconds)
	{
		if (T_value2 < 15℃) then warm_on_off = 1
		else then warm_on_off = 0
	}
}

// 함수2: 현재 온도에 따른 보일러 on/off 함수
AutoStable(int warm_on_off)	//AutoTemp로부터 warm_on_off 변수 받음
{
	if (warm_on_off = 1) then (activate 보일러)
	else (warm_on_off = 0) then (turn off 보일러)
}
```


#### <i class="icon-file"></i> **6. 위험 알람 함수**

_서버의 기능으로 존재하는 각각의 기능에서 위험 상황이 감지되면 이 함수를 통하여 알람이 울리게 된다._

```
// Auto_Temper_Stable Class
Alarm( int alarm )
{
	if alarm=1 then ring alarm
}
Report119( int report )
{
	if report = 1 then ring FireDepartment
    {
		House.GetH_Address();
		House.GetP_Number();
	}
}
```


이상으로 상세 설계 보고를 마칩니다.


