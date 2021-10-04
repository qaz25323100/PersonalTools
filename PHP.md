## require() v.s. include()
  
兩者幾乎一樣，但在錯誤處理的機制不同

## require_once() v.s. require()
  
兩者也一樣，require_once會再多判斷檔案是否有引入  
假如檔案已經引入，就不做任何處理  

## unlink() v.s. unset()
  
unlink()用來刪除檔案  
unset()用來刪除變數內容，在方法裡面只能刪除區域函數  
全域變數需透過unset($GLOBALS['bar'])這種方式來清除變數內容

## 
