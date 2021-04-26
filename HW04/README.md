## HW04 Build a Telegram Chatbot using Amazon API Gateway and AWS Lambda


### 建立function 

1. 建立function <br>
![](https://i.imgur.com/zO4jJoV.png)<br>
2. 上傳檔案 <br>
![](https://i.imgur.com/NjRvpEm.png)<br>
3. 修改eventHandler檔案主程式名稱<br>
![](https://i.imgur.com/npDW8RN.png)<br>

```
//修改格式
你的主程式名稱.處理事件的函式名稱
```
4. 新增layer <br>
如果想要匯入程式語言的某些套件就必須新增layer<br>
a. 在本地建立的個與你函數所用的語言相同名稱的資料夾(例如python)<br>
b. 在該資料夾下載你需要的套件包<br>
```=shell
pip install requests -t .
```
c. 點選新增layer<br>
![](https://i.imgur.com/VwpLD9V.png)<br>
d. 上傳你的套件包.zip(例如python.zip)<br>
e. 回到function主頁新增layer<br>
![](https://i.imgur.com/R178T2V.png)<br>
<br>
5. 新增trigger <br>
照圖中的方式設定即可<br>
![](https://i.imgur.com/vpXkniK.png)<br>
6. 取消代理整合(proxy integration)<br>
a. 點擊藍色字體連結<br>
![](https://i.imgur.com/u8lg2L3.png)<br>
b. 點選整合請求<br>
![](https://i.imgur.com/Uv0pj6I.png)<br>
c. 取消"使用lambda代理整合"<br>
如此API傳回的response會較為精簡<br>
![](https://i.imgur.com/UkgBFIN.png)<br>
d. 做完後記得進行部署<br>
使用default即可<br>
![](https://i.imgur.com/ATK009y.png)<br>
7. 設定參數<br>
a. 複製API endpoit <br>
![](https://i.imgur.com/rs77yNo.png)<br>
b. 貼在config.py裡的WEBHOOK_URL<br>
![](https://i.imgur.com/kFvYbZU.png)<br>
c. 將你的telegram bot的TOKEN貼在config.py<br>
d. 設定完記得點選Deploy!<br>

