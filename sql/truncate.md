# 사용 예시

```sql
select truncate(price, -4) as price_group, count(product_id) as products
from product
group by price_group
order by price_group asc
```

# 용도

- 숫자를 소수 자릿수로 줄이거나 제거하는 데에 사용한다.
    - ex) 10000 이면 1, 1000이면 0이 나온다.
    - ex) 54.29, 1 이면 54.2 이 된다. 