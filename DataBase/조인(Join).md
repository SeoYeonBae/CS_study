# 📌조인(Join)


2개 이상의 테이블이나 데이터베이스를 연결하여 데이터를 검색하는 방법


## 종류

### 내부 조인 (Inner Join)
교집합


### 교차 조인 (Cross Join - cartesin product)
곱집합, 2개 이상의 테이블에 대해 연결 가능한 행을 모두 결합


### 외부 조인 (Outer Join)
2개 이상의 테이블 조인 시 한쪽 테이블의 행에 대해 다른 쪽 테이블에 일치하는 행이 없더라도 다른 쪽 
테이블의 행을 NULL로 하여 행을 return하는 것

         - 완전 외부 조인 (Full Outer Join) : 합집합
         - 왼쪽 (Left Outer Join)
         - 오른쪽 (Right Outer Join)
    
    
### 셀프 조인 (Self Join)
자기자신과 자기자신을 조인하는 것


<hr>

### 참고자료

- [[ Database ] 조인(JOIN)의 종류 - INNER, OUTER, SELF](https://jungeun960.tistory.com/165)
