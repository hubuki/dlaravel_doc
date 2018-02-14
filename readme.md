# 如何使用 dlaravel

* 由於 dlaravel 本身已經是所有的環境，所以其他教學裡面所有灌環境的部分基本上都可以跳過。

***

## 開新的project

* 確認 container 有開啟
```
$ docker ps
``` 

* 開啟 container (若已經開啟請跳過此步驟)
```
$ cd ~/Sites/dlaravel
$ ./console up
```

* 使用 dlaravel 開新的專案 (確認自己在 `~/Sites/dlaravel` 路徑下)
```
$ ./create [project_name]
```

> [project_name] 建議以只有小寫英文、數字、底線三者組成，不可以底線開頭。
> 此指令會一次開好所有的東西，包含網址配對和資料庫。

* 去瀏覽器輸入 `http://[project_name].test:8888` 就能看到新開好的網站，
* 網站程式碼位於 `~/Sites/[project_name]/` 底下

## 已經有寫好的 laravel 專案要 build

* 將專案資料夾放入 `~/Sites/` 底下，並且如果有需要請將專案資料夾重新命名成只有小寫英文、數字、底線組成的名稱。

* 去 `dlaravel` 資料夾建立網址配對和資料庫
```
$ cd ~/Sites/dlaravel
$ ./create --host [project_name]
$ ./create --db [project_name]
```

* 將此專案的程式碼打開，編輯 `.env` 檔案

* 如果沒有請先複製一份出來
```
$ cd ~/Sites/[project_name]
$ cp .env.example .env
```

* 將 `.env` 的部分內容更改為如下
```
APP_URL=http://[project_name].test:8888

DB_CONNECTION=mysql
DB_HOST=db
DB_PORT=3306
DB_DATABASE=[project_name]
DB_USERNAME=[project_name]
DB_PASSWORD=[project_name]
```

* 安裝專案所需套件 (確認自己在 `~/Sites/[project_name]/` 底下)
```
$ dc install
```

* 產生 project key (確認自己在 `~/Sites/[project_name]/` 底下)
```
$ da key:generate
```

* 建制資料表 (必要時使用)
```
$ da migrate
```

* 輸入資料欄位預設值 (必要時使用)
```
$ da db:seed
```

> 以上 2 步驟可以簡化成同一個指令 `da migrate --seed`

* compile 前端資源檔案 (必要時使用)
```
$ npm install
$ npm run dev 或是 gulp 或是其他
```

***

