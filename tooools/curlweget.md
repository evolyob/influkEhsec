```php
-d <data>            //POST的請求中，指定 <data> 到HTTP Server
-H <header/@file>    //GET模式下，指定回傳JSON格式
# curl -H "Content-Type: application/json" www.example.com

curl -k              //****跳過驗證步驟並繼續連線而不進行檢查。
# curl --location --request GET -k 'https://192.168.0.14:12345' 

--output <file>     //將連線的輸出資訊寫到指定的檔案中
# curl -o output.txt https://www.google.com

-u <user:password>   // in server身份驗證
-U <user:password>   // in proxy身份驗證
# curl -u username:password http://example.com

curl -v              //***取得較多的資訊
# curl -v -k https://google.com.tw 2>&1 | grep SSL
####  2>&1  不論出現甚麼都顯示

-X <method>         //指定request的方法，例如：GET、POST、PUT、DELETE
# curl -X POST https://example.com/post/api \ 
# -H 'Content-Type: application/json' \
# -d '{"key_1":"value_1","key_2":"value_2"}'
```
