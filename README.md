# Docker-compose
*start docker-compose*
*--build dùng sau khi chỉnh sửa lại dockerfile và muốn build lại (file: logstash_dockerfile)*
```
$ docker-compose -f elk-compose.yml up --force-recreate -d --build
```

*stop docker-compose*
```
$ docker-compose down
```


# sử dụng filebeat gửi message to logstash
*install filebeat*
```
https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation.html
```
*config filebeat*
```
$ cp filebeat/filebeat.yml /etc/filebeat/filebeat.yml
```
*copy log test*
```
$ cp filebeat_log_test/logstash-tutorial.log /var/log/
```
*status filebeat*
```
$ systemctl status filebeat
```
*start filebeat
```
$ systemctl start filebeat
```
*stop filebeat*
```
$ systemctl stop filebeat
```

*sau khi start filebeat, kiểm tra log container logstash nếu có kết quả như hình "logs_logstash.jpg" là ok*
*có thể thêm -f: Follow log output.(theo dõi log liên tục)*
```
$ docker logs logstash-compose
```

# Lưu ý: 
*filebeat khi thực hiện gửi tin sẽ ghi nhớ offset log line đã được gửi đi, vì vậy có thể khi thực hiện restart filebeat sẽ không thực hiện gửi lại message đã gửi*
*lúc đó logstash không có message để nhận nên kết quả sẽ không giống như hình "logs_logstash.jpg" nữa*
*link tham khảo*
```
https://cuongquach.com/nhung-luu-y-thuong-gap-khi-su-dung-filebeat-gui-log.html
```
*Để gửi lại message cũ để thực hiện test, thực hiện những bước sau*
```
$ systemctl stop filebeat
$ rm -f /var/lib/filebeat/registry/filebeat/data.json
$ systemctl start filebeat
```
