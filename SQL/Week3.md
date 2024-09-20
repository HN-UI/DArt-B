### 문제 1
  
```sql
WITH DEAL_DONE AS (
    SELECT WRITER_ID, PRICE
    FROM USED_GOODS_BOARD
    WHERE STATUS = 'DONE'
)
SELECT USER_ID, NICKNAME, SUM(PRICE) AS TOTAL_SALES
FROM DEAL_DONE JOIN USED_GOODS_USER ON WRITER_ID = USER_ID
GROUP BY USER_ID, NICKNAME
HAVING SUM(PRICE) >= 700000
ORDER BY SUM(PRICE)
```


| WITH 절로 거래 완료된 case의 WRITER_ID와 PRICE만 BOARD에서 추출해 사용했다.  
| WRITER_ID와 USER_ID를 JOIN해서 사용했다.  
| USER_ID와 NICKNAME을 기준으로 GROUP BY 하였고, HAVING절과 SUM()을 사용하여 합계 70만원 이상인 경우만 추출하도록 했다.  



### 문제 2

```sql
WITH NO_CHILD AS (
    SELECT ITEM_ID
    FROM ITEM_TREE
    WHERE ITEM_ID NOT IN (SELECT PARENT_ITEM_ID FROM ITEM_TREE WHERE PARENT_ITEM_ID IS NOT NULL)
)
SELECT I.ITEM_ID, I.ITEM_NAME, I.RARITY
FROM ITEM_INFO I
JOIN NO_CHILD N ON I.ITEM_ID = N.ITEM_ID
ORDER BY I.ITEM_ID DESC;
```


| PARENT_ITEM_ID에 등장하지 않는 ITEM_ID를 찾는 것이 목표인 문제 같은데, WINDOW는 어떻게 써야할지 감이 안잡히네요.. 다른 분들 코드 참고하여 공부하겠습니당 ..  


  
### 문제 3

```sql
SELECT DISTINCT ID, EMAIL, FIRST_NAME, LAST_NAME
FROM DEVELOPERS AS D JOIN SKILLCODES AS S ON S.NAME = 'PYTHON' OR S.NAME = 'C#'
WHERE D.SKILL_CODE & S.CODE > 0
ORDER BY ID
```
  
  
  
  
| SKILLCODES 테이블에서 PYTHON과 C# 코드만 JOIN하고, SKILL_CODE와 CODE를 AND 비트 연산 했을 때 둘 중 하나만 해당 되더라도 0 이상의 값이 나오게 된다.  
| 중복 제거를 위해 DISTINCT를 사용했다.  





<img width="1694" alt="스크린샷 2024-09-20 21 15 44" src="https://github.com/user-attachments/assets/601f88c8-c902-4f4d-872e-7ace69af1a50">


<img width="1705" alt="스크린샷 2024-09-20 21 14 01" src="https://github.com/user-attachments/assets/a1ba1f61-ab09-4deb-9abe-0c4ab51431fb">


<img width="1673" alt="스크린샷 2024-09-20 21 29 09" src="https://github.com/user-attachments/assets/cf0f8549-da45-4c96-88e6-07d921e81772">
