# 哪些學科是學生的感到最難的
=> 查看哪些科目的低分 (L) 比例最高


用xychart
```sql
SELECT 
    Topic, 
    COUNT(*) AS Total_Students,
    SUM(CASE WHEN Class = 'L' THEN 1 ELSE 0 END) AS Low_Grade_Count,
    (SUM(CASE WHEN Class = 'L' THEN 1 ELSE 0 END) / COUNT(*)) * 100 AS Failure_Rate
FROM students_interaction
GROUP BY Topic
ORDER BY Failure_Rate DESC;
```
=> 哪一個科目的「不及格率 (L 等級)」最高

