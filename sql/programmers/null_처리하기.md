```sql
select animal_type, ifnull(name, 'No name') as name, sex_upon_intake
from animal_ins
order by animal_id asc
```

- ifnull 과 nullif 의 차이에 유의해야 한다!
