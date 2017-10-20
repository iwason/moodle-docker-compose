# 概要
Moodleを利用する。  
https://moodle.org/  

## ディレクトリ構成
certs ・・・ssl証明書の配置場所  
moodle ・・・PHP, Apache, moodleインストールを含む  
mysql ・・・MysqlコンテナのVolumeマウント用  
proxy ・・・ リバースプロキシ用　nginx  

## 構築  
### Web２台構成用のプロキシ設定になっているため、以下のコマンドで構築する  
$ docker-compose up -d  --scale moodle=2 


### 環境変数
$ cp moodle.env.example moodle.env  
$ cp mysql.env.example mysql.env  
