# 예시

```sql
select board_id,
       writer_id,
       title,
       price,
       case
           when status = 'SALE'
               then '판매중'
           when status = 'RESERVED'
               then '예약중'
           when status = 'DONE'
               then '거래완료'
           end as status
from used_goods_board
where created_date = '2022-10-05'
order by board_id desc
```

# 문법

```sql
CASE
	WHEN 조건
	THEN '반환 값'
	WHEN 조건
	THEN '반환 값'
	ELSE 'WHEN 조건에 해당 안되는 경우 반환 값'
END AS 나타내고자 하는 컬럼명
```

- case 와 when 은 한 쌍이다
- when 과 then 은 여러개가 존재할 수 있다.
- else 가 존재하면 모든 조건에 해당하지 않는 경우에 반환 값을 설정할 수 있다.
- else 가 없고 어떤 조건에도 해당하지 않는다면 null 을 반환한다.
- end 는 반드시 있어야 한다.
    - end as 와 함께 어떠한 컬럼명으로 나타내고자 하는지 표기하면 된다.