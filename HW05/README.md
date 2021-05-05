
# HW05 Create a Database using Amazon RDS

1. 建立RDS instance<br>
a. 選擇free tier<br>
![](https://i.imgur.com/T84Em5Q.png)<br>
b. 設定instance name與password<br>
![](https://i.imgur.com/KAKpJIK.png)<br>
c. 選擇public access<br>
![](https://i.imgur.com/D16XuBe.png)<br>
d. 其餘皆預設即可<br>
2.新增inbound rules<br>
a. 進入安全群組畫面<br>
![](https://i.imgur.com/vesBm5A.png)<br>
b. 編輯inbound rule<br>
c.type:MySWL/Aurora<br>
  source:"你的ip"<br>
  ip查詢網址:http://checkip.amazonaws.com/<br>
![](https://i.imgur.com/r4pAHej.png)<br>

3.  利用本地python對RDS進行CRUD<br>
a. 將workbench連接至RDS instance<br>
![](https://i.imgur.com/X7TfmKM.png)<br>
設定:<br>
hostname:RDS instance的endpoint<br>
username:你的master user name<br>
password:你當初建立時設定的密碼<br>
b. 從python連接RDS instance<br>
```=python

cnx = mysql.connector.connect(
    host = "RDS instance的endpoint",
    user = "admin",
    password = "密碼"
   
)

print(cnx)
```
c. 建立database<br>
```=python
cursor = cnx.cursor()
sql = "CREATE DATABASE aws_rds_practice;"
print('CREATE DATABASE:',cursor.execute(sql))

```
d. 建立table<br>
``` =python
sql = "CREATE TABLE Persons (PersonID int,LastName varchar(255),FirstName varchar(255),Address varchar(255),City varchar(255));"
print('CREATE TABLE:',cursor.execute(sql))


```
e. 新增資料<br>
``` =python
sql = """
     INSERT INTO Persons(PersonID,LastName,FirstName,Address,City)
     VALUES(%s,%s,%s,%s,%s)
 """
values = (1,'WEI-JIE','TAN','台北市士林區臨溪路70號','台北市')
cursor.execute(sql,values)
cnx.commit()
print('INSERT TABLES:',cursor.rowcount)

```
