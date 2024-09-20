### 문제 1

'''sql
SELECT SELLER_ID, COUNT(DISTINCT ORDER_ID) AS orders
FROM OLIST_ORDER_ITEMS_DATASET
GROUP BY SELLER_ID
HAVING COUNT(DISTINCT ORDER_ID) >= 100
'''
   
**GROUP BY** 와 **HAVING** 사용  

| order_item_id가 있기 때문에 동일한 order_id가 여러 개 존재할 수 있었다. 이걸 생각못하고 DISTINCT를 안 썼다가 여러 번 틀렸다 ..  



### 문제 2

'''sql
SELECT *
FROM tips
WHERE size % 2 != 0
'''  


| where 절에서의 간단한 계산 문제  



### 문제 3

''' sql
WITH tip_sums AS (
    SELECT day, ROUND(SUM(tip), 3) AS tip_daily
    FROM tips
    GROUP BY day
)
SELECT day, tip_daily
FROM tip_sums
WHERE tip_daily = (SELECT MAX(tip_daily) FROM tip_sums);
'''



| WITH 절에서 요일별 팁 합계를 구하고 WHERE 절의 조건문으로 팁 합계가 가장 큰 요일과 이떄의 팁 합계 출력하기
