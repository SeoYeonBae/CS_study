# ๐์กฐ์ธ(Join)


### 2๊ฐ ์ด์์ ํ์ด๋ธ ๋ฐ ๋ฐ์ดํฐ๋ฒ ์ด์ค๋ฅผ ์ฐ๊ฒฐํ์ฌ ๋ฐ์ดํฐ๋ฅผ ๊ฒ์ํ๋ ๋ฐฉ๋ฒ


![image](https://user-images.githubusercontent.com/63834758/210499661-0acdcc03-c305-4d82-a72a-36be52a2764c.png)


<hr>

## ๐ป ๋ด๋ถ ์กฐ์ธ (Inner Join)
- ๊ต์งํฉ
- ์ผ์ชฝ ํ์ด๋ธ๊ณผ ์ค๋ฅธ์ชฝ ํ์ด๋ธ์ ๋ ํ์ด ๋ชจ๋ ์ผ์นํ๋ ๋ถ๋ถ๋ง ํ๊ธฐ

         Select * 
         from tbA A
         inner join tbB B 
         on A.key = B.key



## ๐ป ์ธ๋ถ ์กฐ์ธ (Outer Join)
2๊ฐ ์ด์์ ํ์ด๋ธ ์กฐ์ธ ์ ํ์ชฝ ํ์ด๋ธ์ ํ์ ๋ํด 

๋ค๋ฅธ ์ชฝ ํ์ด๋ธ์ ์ผ์นํ๋ ํ์ด ์๋๋ผ๋ 

๋ค๋ฅธ ์ชฝ ํ์ด๋ธ์ ํ์ NULL๋ก ํ์ฌ ํ์ returnํ๋ ๊ฒ


- **์ผ์ชฝ (Left Outer Join)** : ์ผ์ชฝ ๊ธฐ์ค ๋ถ๋ถ์งํฉ _(์ผ์ชฝ ํ์ด๋ธ์ ๋ชจ๋  ํ์ ๊ฒฐ๊ณผ ํ์ด๋ธ์ ํ๊ธฐ)_

         Select * 
         from tbA A
         left join tbB B 
         on A.key = B.key


- **์ค๋ฅธ์ชฝ (Right Outer Join)** : ์ค๋ฅธ์ชฝ ๊ธฐ์ค ๋ถ๋ถ์งํฉ _(์ค๋ฅธ์ชฝ ํ์ด๋ธ์ ๋ชจ๋  ํ์ ๊ฒฐ๊ณผ ํ์ด๋ธ์ ํ๊ธฐ)_
    
         Select * 
         from tbA A
         right join tbB B 
         on A.key = B.key
    
    

- **์์  ์ธ๋ถ ์กฐ์ธ (Full Outer Join)** : ํฉ์งํฉ

         Select * 
         from tbA A
         full outer join tbB B 
         on A.key = B.key

    
## ๐ป ๊ต์ฐจ ์กฐ์ธ (Cross Join - cartesin product)
๊ณฑ์งํฉ, 2๊ฐ ์ด์์ ํ์ด๋ธ์ ๋ํด ์ฐ๊ฒฐ ๊ฐ๋ฅํ ํ์ ๋ชจ๋ ๊ฒฐํฉ

> _MySQL์ ๊ฒฝ์ฐ cross join = join_

![image](https://user-images.githubusercontent.com/63834758/210502688-9143d802-27ad-4946-9b2d-0e1183d5b9de.png)


    
## ๐ป ์ํ ์กฐ์ธ (Self Join)
์๊ธฐ์์ ๊ณผ ์๊ธฐ์์ ์ ์กฐ์ธํ๋ ๊ฒ



<hr>

### ์ฐธ๊ณ ์๋ฃ

- [[ Database ] ์กฐ์ธ(JOIN)์ ์ข๋ฅ - INNER, OUTER, SELF](https://jungeun960.tistory.com/165)
- [CS ์ ๊ณต์ง์(join)](https://velog.io/@pjh1011409/CS-%EC%A0%84%EA%B3%B5%EC%A7%80%EC%8B%9Djoin)
