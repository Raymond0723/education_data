# => 找出影響成績的『複合型條件』

1.內在行為（舉手 + 看教材）：取其平均值代表「積極度」。  

2.外在約束（缺席天數）：看環境對學生的影響。  

3.最終表現（成績）：看兩者結合後的結果。   

用Bar chart horizental
```sql
SELECT 
    StudentAbsenceDays,
    Class,
    COUNT(*) AS total_students,
    ROUND(AVG(raisedhands), 2) AS avg_raise_hands,
    ROUND(AVG(VisITedResources), 2) AS avg_resources,
    ROUND(SUM(CASE WHEN ParentschoolSatisfaction = 'Good' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS parent_satisfied_pct
FROM students_interaction
GROUP BY StudentAbsenceDays, Class
ORDER BY 
    StudentAbsenceDays DESC, 
    CASE Class WHEN 'H' THEN 1 WHEN 'M' THEN 2 WHEN 'L' THEN 3 END;
```