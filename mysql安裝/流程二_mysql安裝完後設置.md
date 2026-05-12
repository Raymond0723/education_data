# 📊 MySQL 資料庫匯入教學

如何透過命令提示字元 (CMD) 建立資料庫，並將 CSV 資料集匯入 MySQL。

###  啟動 MySQL 並開啟本地匯入權限
在 **CMD** 中輸入以下指令（系統會提示您輸入密碼）：

-- 開啟 cmd 並輸入 (加上 --local-infile 參數以允許本地檔案存取)
```sql
"C:\Program Files\MySQL\MySQL Server 8.0\bin\mysql" -u root -p  
```
-- 1. 建立資料庫
```
CREATE DATABASE IF NOT EXISTS educationdata;
USE educationdata;
```
-- 2. 建立資料表 (根據資料集欄位定義)
```
CREATE TABLE IF NOT EXISTS students_interaction (
    gender VARCHAR(5),
    NationalITy VARCHAR(50),
    PlaceofBirth VARCHAR(50),
    StageID VARCHAR(20),
    GradeID VARCHAR(10),
    SectionID VARCHAR(5),
    Topic VARCHAR(50),
    Semester VARCHAR(5),
    Relation VARCHAR(10),
    raisedhands INT,
    VisITedResources INT,
    AnnouncementsView INT,
    Discussion INT,
    ParentAnsweringSurvey VARCHAR(5),
    ParentschoolSatisfaction VARCHAR(10),
    StudentAbsenceDays VARCHAR(10),
    Class VARCHAR(2)
);
```
-- 3. 全域啟用 local_infile 設定
```
SET GLOBAL local_infile = 1;
LOAD DATA LOCAL INFILE 'C:\\Users\\Raymond\\Desktop\\xAPI-Edu-Data.csv'
INTO TABLE students_interaction
FIELDS TERMINATED BY ',' 
ENCLOSED BY '"' 
LINES TERMINATED BY '\r\n' 
IGNORE 1 ROWS;
```