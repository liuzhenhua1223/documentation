curl -u elastic:Lzh123com -X GET "http://localhost:9200/_cat/indices"

curl -u elastic:Lzh123com -X DELETE "http://localhost:9200/data"

curl -u elastic:Lzh123com -X POST "http://localhost:9200/_snapshot/my_backup/snapshot-2ba8/_restore"



scp -r /app/backup/* 192.168.100.150:/app/backup

2w#E4r%T6y&Uqwas



```apl
curl -u elastic:Lzh123com -X PUT "http://localhost:9200/_snapshot/my_backup" -H 'Content-Type: application/json' -d '{
  "type": "fs",
  "settings": {
    "location": "/app/backup",
    "compress": true
  }
}'

```

![image-20240307111928193](assets2\image-20240307111928193.png)



```apl
curl -u elastic:Lzh123com -X POST "http://localhost:9200/_snapshot/my_backup/snapshot-2ba8/_restore"
```



```
curl -u elastic:Lzh123com -X GET "http://localhost:9200/_cat/indices"

```



![image-20240307112028760](assets2\image-20240307112028760.png)