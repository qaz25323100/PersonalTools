# webpack 與 npm 初始化環境
  
1. 安裝node
2. 建立空的資料夾
3. 進到資料夾，並輸入指令

    npm init -y
 
4. 安裝 webpack, webpack-cli
  
    npm install webpack webpack-cli --save-dev 
  

5. 設置 package.json
      
      "scripts": {  
        "test": "echo \"Error: no test specified\" && exit 1",  
        "build": "webpack" //添加  
      },  
  
# Problems
## npm ERR! Error: EPERM: operation not permitted, rename
