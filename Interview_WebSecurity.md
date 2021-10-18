# XSS

## Store XSS

會被保存在伺服器資料庫中的 JavaScript 代碼引起的攻擊即為 Stored XSS，  
最常見的就是論壇文章、留言板等等，因為使用者可以輸入任意內容，若沒有確實檢查，  
那使用者輸入如 <script> 等關鍵字就會被當成正常的 HTML 執行，標籤的內容也會被正常的作為 JavaScript 代碼執行。
