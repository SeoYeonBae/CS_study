# :pushpin: 정규화(Normalization)

## :computer: 정규화(Normalization)란?

_이상현상이 있는 릴레이션을 분해하여 이상현상을 없애는 과정으로 이상현상이 존재하는 릴레이션을 분해하여 여러 개의 릴레이션을 생성하게 된다_

:heavy_check_mark:  정규화의 장점

- 데이터베이스 변경 시 [이상 현상(Anomaly)](https://github.com/SeoYeonBae/CS_study/blob/main/DataBase/%EC%9D%B4%EC%83%81(Anomaly).md)을 제거할 수 있다.
- 정규화된 데이터베이스 구조에서는 새로운 데이터 형의 추가로 인한 확장 시, 그 구조를 변경하지 않아도 되거나 일부만 변경해도 된다.
- 데이터베이스와 연동된 응용 프로그램에 최소한의 영향만을 미치게 되어 응용프로그램의 생명을 연장시킨다.
   
:heavy_check_mark:  정규화의 단점

- 릴레이션의 분해로 인해 릴레이션 간의 JOIN 연산이 많아진다.
- 질의에 대한 응답 시간이 느려질 수도 있다.
- 만약 JOIN이 많이 발생하여 성능 저하가 나타나면 반정규화(De-normalization)를 적용할 수도 있다.

---

## :computer: 제 1 정규형 (1NF)

:heavy_check_mark: 만족해야 하는 규칙
            
1. 각 컬럼이 하나의 속성만을 가져야 한다.
2. 하나의 컬럼은 같은 종류나 타입(type)의 값을 가져야 한다.
3. 각 컬럼이 유일한(unique)이름을 가져야 한다.
4. 칼럼의 순서가 상관없어야 한다.
             
       
---

## :computer: 제 2 정규형 (2NF)

:heavy_check_mark: 만족해야 하는 규칙
            
1. 1정규형을 만족해야 한다.
2. 모든 컬럼이 부분적 종속(Partial Dependency)이 없어야 한다. == 모든 칼럼이 완전 함수 종속을 만족해야 한다.
           
---

## :computer: 제 3 정규형 (3NF)

:heavy_check_mark:  만족해야 하는 규칙
          
1. 2 정규형을 만족해야 한다.
2. 기본키를 제외한 속성들 간의 이행 종속성 (Transitive Dependency)이 없어야 한다.        

            
---
## :computer: BCNF (Boyce-Codd Normal Form)
:heavy_check_mark:  만족해야 하는 규칙
          
1. 3정규형을 만족해야 한다.
2. 모든 결정자가 후보키 집합에 속해야 한다.
            
---          
        
## :computer: 제 4 정규형 (4NF)         
         
:heavy_check_mark:  만족해야 하는 규칙
           
1. BCNF를 만족해야 한다.
2. 함수 종속이 아닌 다치 종속(MVD: Multi Valued Dependency) 를 제거해야 한다.
           
---          
           
## :computer: 제 5 정규형 (5NF)         

:heavy_check_mark:  만족해야 하는 규칙
          
1. 4정규형을 만족해야 한다.
2. 후보키를 통하지 않는 조인 종속(JD: Join Dependency) 을 제거해야 한다.
         
---

<br>

참고

- https://code-lab1.tistory.com/48
- https://hongcoding.tistory.com/147
