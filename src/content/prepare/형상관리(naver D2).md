#형상관리(naver D2)

참고 - https://youtu.be/ZQ6nrKRju84

**형상 관리(State management)** 가 힘든 가장 큰 이유는 바로 **데이터의 복잡성**

redux -> Apollo, Graphql 로 이동중

### MobX 대신 Redux를 선택한 이유

![스크린샷 2020-06-26 오후 4.55.41](/Users/joseungjin/Library/Application Support/typora-user-images/스크린샷 2020-06-26 오후 4.55.41.png)

![스크린샷 2020-06-26 오후 4.56.21](/Users/joseungjin/Library/Application Support/typora-user-images/스크린샷 2020-06-26 오후 4.56.21.png)

![스크린샷 2020-06-26 오후 4.58.16](/Users/joseungjin/Library/Application Support/typora-user-images/스크린샷 2020-06-26 오후 4.58.16.png)

데이터가 얇은 구조의 데이터가 오지 않을때 (서버에 데이터 가져오기, 중간에 데이터 변경, 변경 후 서버에 보내기 등) 반응형 데이터를 관리하기 위해서는 데이터가 Observable한 형태를 변환시켜야 한다.

- Serialize/Deserialize 할때 고통스러운 현상 -> 계층화가 되어있는 Array 데이터를 손댈때 MobX의 지옥에 빠진다.

### 장점

- 단순하고 이해하기 쉬움 (도입이 빠르고 비동기 처리도 빠름)
- 간편한 비동기 처리
- 클래스와 연결 용이

### 단점

- 서버에서 받아온 자료를 호환 가능한 자료로 변환해야함 (서버에 받아온 자료를 다시 변환 후 서버에 보내야 할때)
- 계층 구조가 깊어질수록 Deserialize 지옥 ( Observable Array = hell )
  - 변환 과정에 프로세스가 느리게 작동 -> 실제 프로젝트에 적용했을때 천개 넘는 데이터가 2~3단계 배열구조라면 자료를 변경시키는 과정에서 어마어마한 지연사항 발생됨 => 실질적으로 효과가 떨어짐
- 에러 컨트롤
  - 내부적으로 자동화 된 부분이 많기 때문에 어느 부분에서 에러가 발생했는지(자료가 깨졌는지) 찾는데 시간이 오래 걸림



![스크린샷 2020-06-26 오후 5.10.14](/Users/joseungjin/Library/Application Support/typora-user-images/스크린샷 2020-06-26 오후 5.10.14.png)

프레임 워크의 가장 큰 트렌드

- 양방향 - 한쪽에서 변화된걸 양쪽에서 동기화 시켜주고 변환 된다는 장점
  - 데이터가 엉키면서 문제가 발생하는 경우가 많음
- 단방향 - 한쪽 방향으로 흐름으로써 생산성을 높이고 오류를 빨리 잡기 위해서는 한쪽으로 흐는게 더 쉽다
  - Make it simple



### Flux

![스크린샷 2020-06-26 오후 5.14.07](/Users/joseungjin/Library/Application Support/typora-user-images/스크린샷 2020-06-26 오후 5.14.07.png)

DDAU - 데이터는 항상 아래로 내려가고 액션은 밑에서 요청하는 방식

원래 있었던 데이터에 원 소스가 변경이 된 자료를 밑으로 내려보낸다.

- 자료의 문제가 생겼을때 원 소스만 한곳에서만 처리가 되면 자동적으로 밑으로 내려가기 때문에 버그를 잡기 좋은 방식 = Redux

![스크린샷 2020-06-26 오후 5.17.58](/Users/joseungjin/Library/Application Support/typora-user-images/스크린샷 2020-06-26 오후 5.17.58.png)

## 액션 Action

type이 있고 그 내용물만 정리해서 전달하는 방식으로 가야함 (action자체는 복잡한 구조가 되어 있으면 안된다 예) 함수를 전달, 클래스 객체를 구성한다던지 -> 안티패턴 )
**무조건 데이터가 쉽게 Serialize 할 수 있는 아주 순수한 형태의 객체 형태만을 전달하는게 목표**

- 무엇을 할지만 정의하고 ~~어떻게 처리할지~~는 포함하지 않음

##리듀서

순수한 함수 - 입력이 있으면 아웃풋이 있고, 아웃풋을 만들어 낼때 앞에 전달받은 액션을 가지고 새 결과를 만들어 낸다.

- 이전 리덕스 스토어 상태와 액션 값으로 새 상태를 생성하는 순수 함수

  ![스크린샷 2020-06-26 오후 5.28.59](/Users/joseungjin/Library/Application Support/typora-user-images/스크린샷 2020-06-26 오후 5.28.59.png)



## 비동기 제어 (미들웨어 선택 장애)

비동기 제어를 어떻게 하느냐 효율적으로 하느냐에 따라서 Redux의 매력이 나온다.

![스크린샷 2020-06-26 오후 5.32.28](/Users/joseungjin/Library/Application Support/typora-user-images/스크린샷 2020-06-26 오후 5.32.28.png)

