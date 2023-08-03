# 📌 해시 맵(Hash Map)

## 🥔 1. 해시맵이란?

- 이름 그대로 해싱된 맵
- 해싱을 사용하기 때문에 많은 양의 데이터를 검색하는데 뛰어남
- Map 인터페이스를 구현한 Map 컬렉션 중 하나
- Map 인터페이스를 상속하고 있기 때문에 Map의 성질을 그대로 가짐

  > ✋ 여기서 잠깐 Map이란?❗</br>
  > 키와 값으로 구성되어 객체를 저장하는 구조의 자료구조</br>
  > 여기서 키와 값은 모두 객체이며, 키는 맵에 유일하게 있어야하고 중복을 허용하지 않음</br>
  > 값은 중복 상관 없으며 같은 키의 값을 삽입하려고 하면 해당 키의 값이 변경됨

  ![image](https://github.com/SeoYeonBae/CS_study/assets/101535851/e9b272f2-f685-490e-93b3-71f055d5daba)

- 그림과 같이 내부에 키와 값을 저장하는 자료구조
- 해시 함수를 통해 티와 값이 저장되는 위치를 결정하므로 그 위치를 알 수 없고 삽입되는 순서와 들어있는 위치 또한 관계가 없음

## 🥔 2. 해시맵 사용해보기

### 1️⃣ 선언

```
import java.util.HashMap;

// Key - Integer, Value - Integer 타입의 Entry를 갖는 HashMap 선언
HashMap<Integer,Integer> map1 = new HashMap<Integer,Integer>();

// New에서 타입 파라미터 생략 가능
HashMap<Integer,Integer> map2 = new HashMap<>();

// 초기 용량(capacity) 지정
HashMap<Integer,Integer> map3 = new HashMap<>(10);

// Key - String, Value - String 타입의 Entry를 갖는 HashMap 선언
HashMap<String,String> map4 = new HashMap<String,String>();

// 초기값 지정
HashMap<String,String> map5 = new HashMap<String,String>(){{
    put("Key1", "Value1");
    put("Key2", "Value2");
}};
```

- 키와 값 타입을 파라미터로 주고 기본 생성자를 호출
- 저장공간보다 값이 추가로 들어오면 List와 같이 저장공간을 추가로 늘림
- 그러나, List처럼 한 칸씩 늘리는 게 아니라 약 두배로 늘리기 때문에 과부하가 많이 발생함
- 그렇기에 초기에 저장할 데이터 개수를 알고 있다면 Map의 초기 용량을 지정해주는 것이 좋음

### 2️⃣ 값 추가

```
// Key - Integer, Value - Integer 타입의 Entry를 갖는 HashMap 선언
HashMap<Integer,String> hm = new HashMap<Integer,String>();

//값 추가
hm.put(1, "One");
hm.put(2, "Two");
hm.put(3, "Three");
hm.put(4, "Four");

//출력결과 : {1=One, 2=Two, 3=Three, 4=Four}
System.out.println(hm);
```

- 키와 값을 파라미터로 주는 Put 메소드를 사용
- 선언 시에 설정한 타입과 같은 타입의 키, 밸류를 넣어야 함
- 입력하는 키 값이 이미 내부에 존재한다면 기존의 값은 새로 입력되는 값으로 변경됨

### 3️⃣ 값 삭제

```
// HashMap 선언, 초기값 지정
HashMap<Integer,String> hm = new HashMap<Integer,String>(){{
    put(1, "One");
    put(2, "Two");
    put(3, "Three");
    put(4, "Four");
}};
hm.remove(1); // key값 1 제거
System.out.println(hm); // 출력결과 : {2=Two, 3=Three, 4=Four}
hm.clear(); // 모든 값 제거
System.out.println(hm); // 출력결과 : {}
```

- 키를 파라미터로 주는 remove(key) 메소드를 사용함
- 모든 값을 제거하려면 crear() 메소드 사용

### 4️⃣ 값 출력

```
// HashMap 선언, 초기값 지정
HashMap<Integer,String> hm = new HashMap<Integer,String>(){{
    put(1, "One");
    put(2, "Two");
    put(3, "Three");
    put(4, "Four");
}};
System.out.println(hm); // 전체 출력 : {2=Two, 3=Three, 4=Four}
System.out.println(hm.get(3)); // Key 값 3의 Value 가져오기 : Three

//entrySet() 활용
for(Map.Entry<Integer,String> entry : hm.entrySet()) {
    System.out.println("Key :" + entry.getKey() + " Value :" + entry.getValue());
}//출력결과
//Key :1 Value :One
//Key :2 Value :Two
//Key :3 Value :Three
//Key :4 Value :Four

//keySet() 활용
for (int i : hm.keySet()) {
    System.out.println("Key :" + i + " Value :" + hm.get(i));
}//출력결과
//Key :1 Value :One
//Key :2 Value :Two
//Key :3 Value :Three
//Key :4 Value :Four
```

- 특정 키의 값 가져오기 : get(key)
- 전체 출력하기 : entrySet() or keySet() 메소드를 활용하여 Map의 객체를 반환받은 후 출력
- entrySet(): Key와 Value로 구성된 Entry의 Set을 받기 대문에 Key와 Value가 모두 필요할 경우 사용
- keySet(): Key의 Set을 반환받기 때문에 Key값만 필요할 경우 사용, 그러나 위의 상황처럼 get(key)를 통해 value를 받아올 수도 있음

  - 다만 이처럼 사용하면 시간이 많이 소모되기 때문에 많은 양의 데이터라면 entrySet이 좋음
 
```
hm.put("파인애플", hm.getOrDefault("파인애플",0)+1);
System.out.println(hm.get("파인애플")); // 출력결과 : 1
```

- key와 defaultValue를 파라미터로 받는 메소드
- 지정된 key에 매핑된 value가 없거나 null이면 defaultValue를 반환하는 메소드
- HashMap에 존재하지(매핑돼있지) 않는 key의 value를 가져오려고 시도하면 defaultValue를 기본값으로 HashMap에 key를 새로 만듦
  
### 5️⃣ 크기 구하기

```
HashMap<Integer,String> hm = new HashMap<Integer,String>(){{
    put(1, "One");
    put(2, "Two");
    put(3, "Three");
    put(4, "Four");
}};
System.out.println(hm.size()); // HashMap 크기 출력 : 4
```

- size() 메소드를 사용해서 구함

### 6️⃣ 특정 키를 포함하는지 여부

```
// HashMap 선언, 초기값 지정
HashMap<Integer,String> hm = new HashMap<Integer,String>(){{
    put(1, "One");
    put(2, "Two");
    put(3, "Three");
    put(4, "Four");
}};
System.out.println(hm.containsKey(4)); // Key 값 4 포함 여부 : true
System.out.println(hm.containsKey(5)); // Key 값 5 포함 여부 : false
```

- containsKey(key) 메소드를 사용
- 존재한다면 true, 존재하지 않는다면 false를 리턴
- 비슷한 메소드로, 특정 value가 존재하는지 확인할 수 있는 containsValue(value) 메소드가 있음

### 7️⃣ HashMap.equals()

```
// HashMap 선언, 초기값 지정
HashMap<Integer,String> hm1 = new HashMap<Integer,String>(){{
    put(1, "One");
    put(2, "Two");
}};
HashMap<Integer,String> hm2 = new HashMap<Integer,String>(){{
    put(1, "One");
    put(2, "Two");
}};
HashMap<Integer,String> hm3 = new HashMap<Integer,String>(){{
    put(1, "One");
    put(3, "Three");
}};
System.out.println(hm1.equals(hm2)); // 출력결과 : true
System.out.println(hm1.equals(hm3)); // 출력결과 : false
```

- equals() 메소드를 사용
- 두 Map의 매핑 상태가 같다면 true, 같지 않다면 false를 리턴

---

##### 참고

- [[Java] 해시맵(HashMap) 자료구조 정리](https://velog.io/@db_jam/Java-%ED%95%B4%EC%8B%9C%EB%A7%B5HashMap-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-%EC%A0%95%EB%A6%AC)
