bin/elasticsearch-certutil ca --pem

unzip certs.zip -d temp

bin/elasticsearch-certutil cert --ca-cert temp/ca/ca.crt --ca-key temp/ca/ca.key --in instance.logstash.yml --out temp/stack.zip --pem

unzip stack.zip -d temp

#convert logstash key as it does not work with the default encryption

openssl pkcs8 -in temp/logstash4/logstash4.key -topk8 -nocrypt -out temp/logstash4/logstash4.pkcs8.key

openssl pkcs8 -in temp/logstash5/logstash5.key -topk8 -nocrypt -out temp/logstash5/logstash5.pkcs8.key

