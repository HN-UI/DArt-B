### 문제 1
  
```sql
SELECT DISTINCT ITEM_ID, ITEM_NAME
FROM ITEM_INFO NATURAL JOIN ITEM_TREE
WHERE PARENT_ITEM_ID IS NULL
ORDER BY ITEM_ID
```


| ID가 NULL 인지 여부를 IS NULL을 통해 확인하여
| ITEM_INFO 테이블과 ITEM_TREE 테이블을 자연 조인하여 사용했다.  



### 문제 2

```sql
SELECT ROUTE, CONCAT(ROUND(SUM(D_BETWEEN_DIST), 1), 'km') AS TOTAL_DISTANCE , CONCAT(ROUND(SUM(D_BETWEEN_DIST)/COUNT(ROUTE), 2), 'km')AS AVERAGE_DISTANCE
FROM SUBWAY_DISTANCE
GROUP BY ROUTE
ORDER BY ROUND(SUM(D_BETWEEN_DIST)) DESC
```


| CONCAT을 통해 결과 값에 'km'을 추가하여 테이블을 구성할 수 있었다.
| 평균은 SUM과 COUNT를 통해 구현하였다.


  
### 문제 3

```sql
WITH PLACECOUNT AS (
    SELECT ID, NAME, HOST_ID, COUNT(NAME) OVER (PARTITION BY HOST_ID) AS NAMECOUNT
    FROM PLACES
)
SELECT ID, NAME, HOST_ID
FROM PLACECOUNT
WHERE NAMECOUNT >= 2
ORDER BY ID;
```

  
  
  
| WINDOW절을 사용하여 NAMECOUNT라는 컬럼을 새로 생성했고, 이를 포함하여 기존 테이블에서 새로운 PLACECOUNT 테이블을 구성했다.
| 여기서 NAMECOUNT를 가지고 헤비 유저를 추출한다.


<img width="587" alt="스크린샷 2024-10-05 21 27 48" src="https://github.com/user-attachments/assets/566e874a-2e9d-4b00-922e-a5098f7070b4">

<img width="1023" alt="스크린샷 2024-10-05 21 38 22" src="https://github.com/user-attachments/assets/e1c4c99e-95ff-478b-b5d9-b2cba2ef52d0">

<img width="1008" alt="스크린샷 2024-10-05 21 45 17" src="https://github.com/user-attachments/assets/da3dbcda-ddce-4928-93ee-cd18a1c74a23">
