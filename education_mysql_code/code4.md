# 呈上code3

透過將舉手次數（raisedhands）進行區間分組，成功找出了決定成績的「關鍵門檻」  


```sql
SELECT 
    CASE 
        WHEN raisedhands >= 75 THEN '75+ (極高主動)'
        WHEN raisedhands >= 50 THEN '50-74 (高主動)'
        WHEN raisedhands >= 25 THEN '25-49 (中主動)'
        ELSE '0-24 (低主動)' 
    END AS activity_level,
    COUNT(*) AS total_students,
    -- 計算該區間拿到 H 的比例
    ROUND(SUM(CASE WHEN Class = 'H' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS chance_of_H,
    -- 計算該區間拿到 L 的比例
    ROUND(SUM(CASE WHEN Class = 'L' THEN 1 ELSE 0 END) * 100.0 / COUNT(*), 2) AS chance_of_L
FROM students_interaction
GROUP BY activity_level
ORDER BY MIN(raisedhands) DESC;
```