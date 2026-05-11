# 🚻 性別與學科傾向觀察 (Gender & Subject Engagement)

在教育數據分析中，我們經常探討：**不同性別對不同學科的興趣分布以及實際的課堂表現是否存在差異？**

---

### 🛠️ SQL 查詢分析
選取了「學科 (Topic)」與「性別 (Gender)」作為維度，計算學生人數與**平均參與度 (舉手次數)**：

--使用面板 Bar chart horizental
```sql
SELECT 
    Topic, 
    gender, 
    COUNT(*) AS student_count, 
    AVG(raisedhands) AS avg_engagement
FROM students_interaction
GROUP BY Topic, gender
ORDER BY Topic, gender;
```

因為觀察不明顯所以降續排列  
-- DESC 代表從高到低排列
```sql
SELECT 
    Topic, 
    gender, 
    COUNT(*) AS student_count, 
    AVG(raisedhands) AS avg_engagement
FROM students_interaction
GROUP BY Topic, gender
ORDER BY avg_engagement DESC;  
```