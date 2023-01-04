# 📌조인(Join)


### 2개 이상의 테이블 및 데이터베이스를 연결하여 데이터를 검색하는 방법


![image](https://user-images.githubusercontent.com/63834758/210499661-0acdcc03-c305-4d82-a72a-36be52a2764c.png)


<hr>

## 💻 내부 조인 (Inner Join)
- 교집합
- 왼쪽 테이블과 오른쪽 테이블의 두 행이 모두 일치하는 부분만 표기

         Select * 
         from tbA A
         inner join tbB B 
         on A.key = B.key



## 💻 외부 조인 (Outer Join)
2개 이상의 테이블 조인 시 한쪽 테이블의 행에 대해 

다른 쪽 테이블에 일치하는 행이 없더라도 

다른 쪽 테이블의 행을 NULL로 하여 행을 return하는 것


- **왼쪽 (Left Outer Join)** : 왼쪽 기준 부분집합 _(왼쪽 테이블의 모든 행을 결과 테이블에 표기)_

         Select * 
         from tbA A
         left join tbB B 
         on A.key = B.key


- **오른쪽 (Right Outer Join)** : 오른쪽 기준 부분집합 _(오른쪽 테이블의 모든 행을 결과 테이블에 표기)_
    
         Select * 
         from tbA A
         right join tbB B 
         on A.key = B.key
    
    

- **완전 외부 조인 (Full Outer Join)** : 합집합

         Select * 
         from tbA A
         full outer join tbB B 
         on A.key = B.key

    
## 💻 교차 조인 (Cross Join - cartesin product)
곱집합, 2개 이상의 테이블에 대해 연결 가능한 행을 모두 결합

> _MySQL의 경우 cross join = join_

![image](https://user-images.githubusercontent.com/63834758/210502688-9143d802-27ad-4946-9b2d-0e1183d5b9de.png)


    
## 💻 셀프 조인 (Self Join)
자기자신과 자기자신을 조인하는 것



<hr>

### 참고자료

- [[ Database ] 조인(JOIN)의 종류 - INNER, OUTER, SELF](https://jungeun960.tistory.com/165)
- [CS 전공지식(join)](https://velog.io/@pjh1011409/CS-%EC%A0%84%EA%B3%B5%EC%A7%80%EC%8B%9Djoin)
