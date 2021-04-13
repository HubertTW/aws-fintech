## HW03  Build a Website using Amazon S3(Versioning) and AWS Amplify
網頁部署的方式有非常多種,我們可以依照每個專案的需求使用不一樣的服務.<br>


### 使用S3部署靜態公開網頁



1. 建立一個S3 bucket(皆為預設值)<br>
2. 將靜態網頁從local pc上傳<br>
3. 開啟bucket-versioning<br>
![](https://i.imgur.com/r1TF0Ho.png)<br>
4. 上傳新版本的檔案(記得打開list-version)<br>
5. 設定預設首頁<br>
![](https://i.imgur.com/yVSsznP.png)<br>
6. 開啟所有權限<br>
7. 新增policy<br>
resource 記得改成自己的bucket arn<br>
![](https://i.imgur.com/sn51F3G.png)<br>
```

{
  "Version":"2012-10-17",
  "Statement":[
    {
      "Sid":"PublicRead",
      "Effect":"Allow",
      "Principal": "*",
      "Action":["s3:GetObject","s3:GetObjectVersion"],
      "Resource":["arn:aws:s3:::aws-fintech-hw03"]
    }
  ]
}

```
8. 將網站設為公有<br>
![](https://i.imgur.com/PCgPW6X.png)<br>

* 我們可以使用S3提供的API來設計檔案上傳相關的功能<br>
https://boto3.amazonaws.com/v1/documentation/api/latest/reference/services/s3.html<br>



### 使用AWS Amplify建立靜態網頁<br>
1. 使用amplify建立一個新的app<br>
使用github的方式進行版本管理<br>
![](https://i.imgur.com/zEa1pnV.png)<br>
2. 部署完成<br>