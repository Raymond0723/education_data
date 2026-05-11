# 🔍 關鍵行為分析：哪種行為最能預測「高分」？

### ❓ 分析目標
想找出：**舉手次數、看教材次數、看公告、參與討論**，哪一個動作跟最終成績 (**H**igh / **M**edium / **L**ow) 最相關？

---

### 💻 SQL 查詢指令
透過計算各成績族群在各項指標上的平均值，來觀察行為差異：


--使用面板 Bar chart
```sql
SELECT 
    Class, 
    AVG(raisedhands) AS avg_raise_hands, 
    AVG(VisITedResources) AS avg_visit_res, 
    AVG(AnnouncementsView) AS avg_view_announcement, 
    AVG(Discussion) AS avg_discussion
FROM students_interaction
GROUP BY Class
ORDER BY 
    CASE Class WHEN 'H' THEN 1 WHEN 'M' THEN 2 WHEN 'L' THEN 3 END;