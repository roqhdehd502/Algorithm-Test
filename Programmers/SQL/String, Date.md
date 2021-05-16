## 1. 루시와 엘라 찾기

```sql
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ('Lucy', 'Ella', 'Pickle', 'Rogan', 'Sabrina', 'Mitty')
ORDER BY ANIMAL_ID ASC;
```

## 2. 이름에 el이 들어가는 동물 찾기

```sql
SELECT animal_id, name
FROM animal_ins
WHERE upper(name) like upper('%el%')  and animal_type like 'Dog'
ORDER BY name;
```

## 3. 중성화 여부 파악하기

```sql
SELECT ANIMAL_ID, NAME, 
    CASE
        WHEN SEX_UPON_INTAKE LIKE 'Neutered Male' THEN 'O'
        WHEN SEX_UPON_INTAKE LIKE 'Spayed Female' THEN 'O'
        ELSE 'X'
    END AS "중성화"
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID ASC;
```

## 4. 오랜 기간 보호한 동물(2)

```sql
SELECT ANIMAL_ID, NAME
FROM
(
    SELECT A.ANIMAL_ID, A.NAME , B.DATETIME - A.DATETIME AS HOUR
    FROM
    ANIMAL_INS A LEFT OUTER JOIN ANIMAL_OUTS B
    ON A.ANIMAL_ID = B.ANIMAL_ID
    WHERE B.DATETIME - A.DATETIME IS NOT NULL
    ORDER BY HOUR DESC
)
WHERE ROWNUM < 3
```

## 5. DATETIME에서 DATE로 형 변환

```sql
SELECT ANIMAL_ID, NAME, TO_CHAR(DATETIME, 'YYYY-MM-DD') AS "날짜"
FROM ANIMAL_INS 
ORDER BY ANIMAL_ID ASC;
```

