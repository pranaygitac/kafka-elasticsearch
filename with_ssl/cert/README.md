#https://www.elastic.co/blog/configuring-ssl-tls-and-https-to-secure-elasticsearch-kibana-beats-and-logstash

bin/elasticsearch-certutil cert  --keep-ca-key --pem --in instance.yml --out certs.zip

unzip certs.zip -d temp

openssl pkcs8 -in temp/logstash4/logstash4.key -topk8 -nocrypt -out temp/logstash4/logstash4.pkcs8.key
openssl pkcs8 -in temp/logstash5/logstash5.key -topk8 -nocrypt -out temp/logstash5/logstash5.pkcs8.key

ls temp/logstash*

docker cp instance.yml es01:/usr/share/elasticsearch/

docker cp  es01:/usr/share/elasticsearch/temp cert/

curl -v --cacert elastic/with_ssl/cert/ca/ca.crt  https://logstash4.com:5049
