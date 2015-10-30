# checkfreespace


  ## AWSの構成

*** APIGateway ・・・デバイス側やHTMLから呼び出されるＡＰＩ群 ***

*** Lambda・・・デバイス管理のビジネスロジック ***

*** S3・・・デバイスの状態、デバイス登録などが可能な管理画面ＨＴＭＬ ***

*** DyanamoDB・・・デバイス管理 ***

#### APIGateway
---------------------------------

_サーバにデバイスの情報を送る。_
```
method: setdevice

parameters: status
            0・・・誰も人がいないはず
            1・・・誰か人がいるはず
            deviceid このマシンのデバイスＩＤ
action: get

response :
  type json
  example {"result":0}
  result 0 登録成功  999　登録失敗

```

   _サーバから自デバイスの情報をもらう_
```
method: getdevice
parameters: deviceid このマシンのデバイスＩＤ
action: get
response : type json
           example
           {
             "Item": {
               "devicename": "4001",
               "reserved": 0,
               "alert": 0,
               "deviceid": "4F001",
               "status": 0
             }
           }
           alert 0 何もなし 1 アラートならして！
           status 0 未使用 1 使用中

```

#### S3
---------------------------------
 bucket名: checkfreespace

 権限：社内のみアクセス可能

**index.html**　・・・　フリースペースすべての情報が表示される。


#### DynamoDB
---------------------------------
 table: cfdevice
　　deviceid String
    devicename String
    status Number
    alert Number
    reserved Number
