# 2️⃣ 프리코스 2주차 java-racingcar-precourse

## ✨기능
초간단 자동차 경주 게임을 구현한다.

주어진 횟수 동안 n대의 자동차는 전진 또는 멈출 수 있다.
각 자동차에 이름을 부여할 수 있다. 전진하는 자동차를 출력할 때 자동차 이름을 같이 출력한다.
자동차 이름은 쉼표(,)를 기준으로 구분하며 이름은 5자 이하만 가능하다.
사용자는 몇 번의 이동을 할 것인지를 입력할 수 있어야 한다.
전진하는 조건은 0에서 9 사이에서 무작위 값을 구한 후 무작위 값이 4 이상일 경우이다.
자동차 경주 게임을 완료한 후 누가 우승했는지를 알려준다. 우승자는 한 명 이상일 수 있다.
우승자가 여러 명일 경우 쉼표(,)를 이용하여 구분한다.
사용자가 잘못된 값을 입력할 경우 IllegalArgumentException을 발생시킨 후 애플리케이션은 종료되어야 한다.

## 🌟 구현 기능 목록
1. 입출력
    - [x] 입력 포맷 지정
    - [x] 자동차 이름 입력(쉼표로 구분)
    - [x] 시도 횟수 입력
    - [x] 게임 결과 출력 포맷 지정
    - [x] 실행 결과 출력
    - [x] 우승자 출력
2. 입력값 유효성 검사
    - [x] 자동차 이름 유효성 검사
    - [x] 시도 횟수 유효성 검사
3. 자동차
    - [x] Cars 객체에서 자동차 이름 리스트 생성
    - [x] 자동차 별로 0에서 9 사이에서 랜덤 값 생성
4. 자동차 경주 게임 진행
    - [x] 시도 횟수만큼 게임 진행
    - [x] 자동차 별 랜덤 값 생성 
    - [x] 랜덤 값이 4 이상이면 전진값 저장
    - [x] 시도 횟수만큼 게임 진행
    - [x] 전진값이 가장 큰 자동차 판별
---

## ♼ MVC 패턴
이번 2주차 미션은 MVC 패턴의 본질을 잘 이해해보고자 MVC 패턴으로 구현하였습니다.

MVC 패턴을 활용해 각 컴포넌트의 역할을 명확하게 나누어 구현하다보니 1주차에 비해 코드를 직관적으로 이해할 수 있었고, 유지보수하기 훨씬 편리하다는 것을 느꼈습니다.

단일 책임의 원칙뿐만 아니라 각 메서드 별로 최소한의 기능만을 담당하게 하여 나중에 게임 규칙이 변경되더라도 최소한의 수정으로도 변경이 가능하도록 하였습니다.

### 📍Model

`Model`은 애플리케이션의 핵심 데이터와 비즈니스 로직을 포함하는 부분입니다.
`Car`, `Cars`, `RacingGame` 클래스에서 게임 로직을 담당하도록 설계해 게임의 규칙과 데이터 변경을 독립적으로 관리하게 하였습니다. 
또한 `RandomNumGenerator` 클래스에서 난수 생성 책임만을 담당하게 하였습니다.

### 📍View

`View`는 사용자에게 보여지는 부분으로, `Input`과 `Output` 클래스를 통해 입력과 출력을 담당합니다. 
MVC 패턴에서 `View`는 데이터의 표현과 사용자와의 상호작용을 담당하므로, `Model`과 `Controller`와의 강한 결합을 피해야 한다는 점을 이번 미션에서 더 깊이 이해하게 되었습니다. 
`Output` 클래스에서 출력 형식을 관리하고 `Input` 클래스에서 사용자 입력을 처리함으로써, 게임의 로직과는 분리된 깔끔한 입출력 코드를 작성할 수 있었습니다.

### 📍Controller

`Controller`는 `Model`과 `View`를 연결하는 역할을 담당합니다. 
`RacingCarController` 클래스를 통해 게임의 흐름을 제어하고, `Input`으로부터 받은 데이터를 `Model`로 전달하고 `Output`으로 결과를 보여주는 식으로 설계했습니다. 
`Controller`에서 `Model`과 `View` 간의 상호작용을 관리하면서, 두 컴포넌트가 서로 의존하지 않도록 설계하는 것이 MVC 패턴의 핵심이라는 것을 배우게 되었습니다. 특히, 게임의 시도 횟수와 우승자 결정 등의 로직을 `Controller`에서 처리하여, 게임 진행과 관련된 책임이 분리되는 것을 경험할 수 있었습니다.

### ✅ 테스트 코드
MVC 패턴으로 각각의 구성 요소가 독립적으로 작동하도록 설계되어, 테스트 코드 작성이 상대적으로 수월했습니다. Model의 핵심 로직은 독립적이어서 테스트가 용이했고, View의 입출력 테스트도 Mocking 없이 간단히 구현할 수 있었습니다.