# ELK Stack
- E = Elasticsearch
- L = Logstash
- K = Kibana

## Deploy on Docker

```
mkdir -p es_data
chown 1000.1000 es_data
docker-compose up -d
```

## หมายเหตุ

ใช้งานในระบบที่ต้องรับโหลดมากๆ อย่างน้อยๆต้องใช้ `network_mode: host` และต้องแก้ `elasticsearch` โฮสต์ให้เป็น IP ของเครื่อง Server หรือใช้ `127.0.0.1` ได้ ถ้ารันบนเครื่องเดียวกัน

## Error ที่อาจจะเจอ
- Shards เต็ม ต้องแก้ผ่าน REST API ของ Elasticsearch

วิธีแก้

```
curl -XPUT $ES:9200/_cluster/settings -H 'Content-type: application/json' -d '{"transient":{"cluster.max_shards_per_node":9999}}'
```

- เรื่องของ Memory

> https://www.elastic.co/guide/en/elasticsearch/reference/current/heap-size.html

