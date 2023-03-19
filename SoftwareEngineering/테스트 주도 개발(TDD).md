# :pushpin: 테스트 주도 개발(TDD)

_소프트웨어 개발 프로세스에서 새로운 코드를 작성하기 전에 자동화된 테스트 케이스를 작성하는 것을 중심으로 한 개발 방법론_

## :computer: TDD의 기본 개념

:heavy_check_mark: TDD란?

- **T**est **D**riven **D**evelopment의 약자로 ‘테스트 주도 개발’이라고 함
- 짧은 개발 주기의 반복에 의존하는 개발 프로세스
- 애자일 방법론 중 하나인 XP의 Test-First 개념에 기반을 둔 단순한 설계를 중요시 함

:heavy_check_mark: XP란?

- eXtream Programming
- 미래에 대한 예측을 최대한 하지 않고 지속적으로 프로토타입을 완성하는 애자일 방법론 중 하나
- 추가 요구사항이 생기더라도 실시간으로 반영 가능

:heavy_check_mark: TDD의 과정

![image](https://user-images.githubusercontent.com/69101568/226177353-7f582cc8-8818-42f0-98fa-f8dc39987cff.png)

1. 실패하는 작은 테스트 코드를 작성
2. 새로운 코드를 작성하여 테스트를 통과시킴
3. 코드 개선과 중복 제거 (리팩토링)
4. 위 과정을 반복

TDD를 통해 코드의 **안정성과 유지보수성**을 높일 수 있다!!!

---

## :computer: TDD의 장점

- 코드의 품질을 높일 수 있음
- 버그를 미리 찾을 수 있음
- 리팩토링을 용이하게 할 수 있음
- 코드의 이해도와 유지보수성을 높일 수 있음
- 팀 전반의 코드 품질을 향상시킬 수 있음

---

## :computer: TDD의 단점

- 초기 개발 단계에서는 시간이 많이 걸림
- 테스트 코드의 작성과 유지보수에 대한 추가적인 노력이 필요함
- 완벽한 테스트 케이스를 작성하기 어려움

---

## :computer: TDD의 주요 도구

- xUnit
- JUnit
  - 현재 전 세계적으로 가장 널리 사용되는 java 단위 테스트 프레임 워크
- NUnit
- PHPUnit

---

## :computer: 좋은 테스트의 5가지 규칙 (FIRST)

1. Fast: 테스트는 빠르게 동작하여 자주 돌릴 수 있어야 한다.
2. Independent: 각각의 테스트는 독립적이며 서로 의존해서는 안된다.
3. Repeatable: 어느 환경에서도 반복 가능해야 한다.
4. Self-Validating: 테스트는 성공 또는 실패로 bool 값으로 결과를 내어 자체적으로 검증되어야 한다.
5. Timely: 테스트는 적시에 즉, 테스트하려는 실제 코드를 구현하기 직전에 구현해야 한다.

---

<br>

참고

- [TDD란? 테스트 주도 개발](https://hanamon.kr/tdd%EB%9E%80-%ED%85%8C%EC%8A%A4%ED%8A%B8-%EC%A3%BC%EB%8F%84-%EA%B0%9C%EB%B0%9C/)
- [[TDD] 단위 테스트와 TDD(테스트 주도 개발) 프로그래밍 방법 소개 - (1/5)](https://mangkyu.tistory.com/182)
- [TDD, 테스트 주도 개발이란?](https://velog.io/@wngud4950/TDD%EB%9E%80)
