

https://medium.com/@g4b1s/setting-up-ssl-for-filebeat-and-logstash-9d0866f76881

cp /etc/ssl/openssl.cnf my_openssl_logstash.cnf

#Edit my_openssl.cnf file #In v3_ca topic, replace

[ v3_ca ] subjectAltName = IP: YOUR_SERVER_IP

#with

[ v3_ca ] subjectAltName = IP: 10.256.30.21

openssl req -x509 -batch -nodes -days 3650 -newkey rsa:2048 -keyout logstash.key -out logstash.crt -config my_openssl_logstash.cnf

curl -v --cacert cert/logstash.crt https://10.51.96.67:5049
