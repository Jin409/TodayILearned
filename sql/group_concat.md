```SQL
GROUP_CONCAT
([ DISTINCT] expr [,expr ...]
    [ORDER BY {unsigned_integer | col_name | expr} [ASC | DESC] [,col_name ...]]
    [SEPARATOR str_val])
 ```

- DISTINCT 로 중복된 값을 제거한다.
- expr 로 결합될 열을 지정한다.
- ORDER BY 결합할 열의 정렬 순서를 지정한다.
- SEPARATOR 결합할 열 사이의 구분자를 삽입한다.

```SQL
SELECT ID,
       EMAIL,
       GROUP_CONCAT(DISTINCT NAME, CATEGORY) AS GROUPED
FROM SKILLCODES
         JOIN
     DEVELOPERS
     ON DEVELOPERS.SKILL_CODE & SKILLCODES.CODE
GROUP BY 1, 2
```

이렇게 쿼리문을 작성하게 되면, NAME 의 중복 없이 name 과 category 를 하나의 문자열로 합쳐서 나타내겠다는 의미이다.

