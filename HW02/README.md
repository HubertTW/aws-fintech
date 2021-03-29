
# HW2 Build a Website using Amazon EC2 with LAMP
在這邊使用的是node.js+MySQL




## 建置EC2並遠端連線

事前準備:
* 安裝好puTTY & PuTTYgen
*  具備aws認證帳號





1. 建構ec2 instance
a. 點選啟動執行個體
![](https://i.imgur.com/lk6XIqC.png)
b. 點選Amazon Linux 2 AMI (HVM),SSD Volume Type 
![](https://i.imgur.com/uktphBJ.png)
c. 點選t2 micro
![](https://i.imgur.com/m3eCsi8.png)
d. 在step 7 前都默認即可
e. 最後點下launch時,會跳出詢問是否產生新的金鑰對
如果有現有的就用現有的,沒有的話就產生新的並下載.
![](https://i.imgur.com/oXZ9pF1.png)

2. 產生.ppk金鑰 <br>
import 剛剛在ec2產生的金鑰
![](https://i.imgur.com/l5A60u5.png)


3. 連線ec2主機 <br>
a. 匯入.ppk金鑰 <br>
開啟putty--> <br>
點選SSH--> <br>
點選Auth--> <br>
把剛剛產生的.ppk金鑰匯進來 <br>
![](https://i.imgur.com/tk0CABq.png =500x500)
b. 連線EC2 <br>
把EC2上public IP寫入PuTTy--> <br>
Save--> <br>
open--> <br>
輸入ec2-user
![](https://i.imgur.com/fiVo6Vp.png)
![](https://i.imgur.com/5NGWUhg.png)




## 在EC2上架node.js

1. 新增inbound rules <br>
點選安全群組--> <br>
點選傳入規則--> <br>
點選編輯傳入規則--> <br>
新增一個規則--> <br>
設定如下: <br>
port:3000 <br>
類型:客製 TCP <br>
來源:0.0.0.0/0 <br>
2. 將你的index.js檔案上傳上去
```=js
//index.js
var express=require("express");
var app = express();//產生express app物件
app.get("/",function(req,res){
	res.send("HW02 deploy nodejs on ec2 by 資四B 06156221 張恩睿");
	
});
app.get("/mypath",function(req,res){
	
	res.send("this is my path");
});


app.listen(3000,function(){
	console.log("伺服器已啟動");
	
});



```
4. 執行 index.js 伺服器
```
$node index.js
```
4. 進入網站:http://54.221.53.239:3000

## 在RDS上架MySQL


1. 進入RDS頁面 <br>
點選create database
![](https://i.imgur.com/RCbKTVR.png)

2. 規格設定 <br>
點選easy create
![](https://i.imgur.com/D6y2Ked.png)
設定database identifier
設定username
設定password
![](https://i.imgur.com/vpcCIwU.png)

3. 建置database.js

```=js
//database.js
var mysql      = require('mysql');
var connection = mysql.createConnection({
  host     : '你的host',
  user     : '你的名稱',
  password : '你的密碼',
});

connection.connect((err) => {
    if (err) throw err;
    console.log('Connected!');
    
  });

```

4. 進行連線
```
node database.js
```
顯示Connected就是成功了!
![](https://i.imgur.com/aM9FC0P.png)




ref:
1. [node.js安裝](https://learningsky.io/aws-ec2-ubuntu-vm-install-nvm-nodejs-express/)
2. [MySQL安裝](https://stackabuse.com/using-aws-rds-with-node-js-and-express-js/)
