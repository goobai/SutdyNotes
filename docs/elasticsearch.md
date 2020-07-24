# elasticsearch

## docker compose配置集群

```shell script
version: '2.2'
services:
  es01:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.7.0
    container_name: es01
    environment:
      - node.name=es01
      - cluster.name=es-docker-cluster
      - discovery.seed_hosts=es02,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data01:/usr/share/elasticsearch/data
    ports:
      - 9200:9200
    networks:
      - elastic
  es02:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.7.0
    container_name: es02
    environment:
      - node.name=es02
      - cluster.name=es-docker-cluster
      - discovery.seed_hosts=es01,es03
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data02:/usr/share/elasticsearch/data
    networks:
      - elastic
  es03:
    image: docker.elastic.co/elasticsearch/elasticsearch:7.7.0
    container_name: es03
    environment:
      - node.name=es03
      - cluster.name=es-docker-cluster
      - discovery.seed_hosts=es01,es02
      - cluster.initial_master_nodes=es01,es02,es03
      - bootstrap.memory_lock=true
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    ulimits:
      memlock:
        soft: -1
        hard: -1
    volumes:
      - data03:/usr/share/elasticsearch/data
    networks:
      - elastic
  kibana:
    image: kibana:7.7.0
    container_name: kibana
    restart: always
    ports:
      - "5601:5601"
    environment:
      I18N_LOCALE: zh-CN #汉化
    networks:
      - elastic
    links:
      - es01:elasticsearch
volumes:
  data01:
    driver: local
  data02:
    driver: local
  data03:
    driver: local

networks:
  elastic:
    driver: bridge
```

## 修改 vm.max_map_count

```shell script
    vi /etc/sysctl.conf
    //修改为下面内容
    # sysctl settings are defined through files in
    # /usr/lib/sysctl.d/, /run/sysctl.d/, and /etc/sysctl.d/.
    #
    # Vendors settings live in /usr/lib/sysctl.d/.
    # To override a whole file, create a new file with the same in
    # /etc/sysctl.d/ and put new settings there. To override
    # only specific settings, add a file with a lexically later
    # name in /etc/sysctl.d/ and put new settings there.
    #
    # For more information, see sysctl.conf(5) and sysctl.d(5).
    fs.inotify.max_user_instances=524288
    vm.max_map_count=262144

```

## 启动容器

```shell script
docker-compose up -d
```

## 测试是否启动成功

```shell script
    curl -X GET "localhost:9200/_cat/nodes?v&pretty"
    //输出
    ip         heap.percent ram.percent cpu load_1m load_5m load_15m node.role master name
    172.21.0.3           17          97   3    0.01    0.40     0.45 dilmrt    -      es02
    172.21.0.4           54          97   3    0.01    0.40     0.45 dilmrt    -      es03
    172.21.0.2           67          97   3    0.01    0.40     0.45 dilmrt    *      es01

```
