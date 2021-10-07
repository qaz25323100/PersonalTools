## Common JS vs AMD vs ES6(ES2015,native javascript)
https://zhuanlan.zhihu.com/p/158683510

## 箭頭函數(ES6)

    const plus = function(num1+num2){
        return num1+num2; 
    }
  
利用箭頭函數可以寫作  
  
    const plus = (num1+num2) => {
        return num1+num2; 
    }
  
或是  
  
    const plus = (num1+num2) => num1+num2; 

※當只有一個參數的時候  
  
    const plus = num1 => console.log(msg);
