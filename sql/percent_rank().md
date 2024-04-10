# 상위 퍼센트 구하기
```sql
SELECT *
FROM (
    SELECT percent_rank() OVER (ORDER BY size_of_colony DESC) AS percent
    FROM ecoli_data
) AS ranked_data
WHERE percent <= 0.01;
```
- percent_rank() 함수를 이용하면 퍼센트를 구할 수 있다.
- size_of_colony 를 역순으로 정렬한 것이므로, 위의 쿼리와 같이 실행하면 상위 1퍼센트의 데이터를 볼 수 있게 된다.
- 집계함수이므로 바로 where 절에서 사용할 수는 없다.

# 그룹별 상위 퍼센트 구하기
```sql
SELECT *
FROM (SELECT total_bill, sex, 
      PERCENT_RANK() OVER (PARTITION BY sex ORDER BY total_bill DESC) as per_rank FROM tips) a
WHERE a.per_rank <= 0.02;
```
- partition by 로 그룹별로 구할 수 있게 된다.
   - sex 별로 구하게 된다.
