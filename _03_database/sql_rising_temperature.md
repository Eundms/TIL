> 전 날보다 온도가 더 높은 날의 id 값 구하기

```sql
select id
    from weather join weather w
    on DATEDIFF(weather.recordDate, w.recordDate) = 1
    and weather.Temparature > w.Temparature
;
```