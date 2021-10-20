# XSS

## Store XSS

會被保存在伺服器資料庫中的 JavaScript 代碼引起的攻擊即為 Stored XSS，  
最常見的就是論壇文章、留言板等等，因為使用者可以輸入任意內容，若沒有確實檢查，  
那使用者輸入如 <script> 等關鍵字就會被當成正常的 HTML 執行，標籤的內容也會被正常的作為 JavaScript 代碼執行。


## Reflected XSS
  
Reflected 是指不會被儲存在資料庫中，而是由網頁後端直接嵌入由前端使用者所傳送過來的內容造成的，  
最常見的就是以 GET 方法傳送資料給伺服器時，伺服器未檢查就將內容回應到網頁上所產生的漏洞。
  
![image](https://user-images.githubusercontent.com/7361217/137661798-b62799ed-2ebe-4fa6-9e84-943208266d17.png)

# SQL Injection
 
透過網頁中使用者所輸入的資料，進而存取資料庫資料的功能。  

如底下Select後台使用者資訊  
  
    String queryStr = "SELECT * FROM person WHERE account = " + "'" + account + "'" + " AND password = " +  "'" + password + "'"
  
如果使用者密碼輸入為 ** ' OR 1 = 1 -- **，
  
    SELECT * FROM user WHERE account = 'Kenny@example.com' AND password = '' OR 1 = 1 --'

這樣的SQL條件就會把account的所有數據印出來  

## 防範


