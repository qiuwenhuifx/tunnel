# 同步到kafka配置

如下面的配置文件，配置了一个把 test.student_name 中的实时数据同步到kafka中student_name_logs的topic中

```json
{
    # pg_dump 可执行文件path，如pg_dump在 $PATH 路径下面，则不需配置
    "pg_dump_path": "",
    "subscribes": [{
        # 是否dump 历史数据，如只需要实时数据，可以不配或配置为false，默认false
        "dump": false,
        # 逻辑复制槽名称，确保唯一
        "slotName": "slot_for_kafka",
        # pg 连接配置
        "pgConnConf": {
            "host": "127.0.0.1",
            "port": 5432,
            "database": "test",
            "user": "postgres",
            "password": "admin"
        },
        # 同步规则配置
        "rules": [
            {
                # 表名匹配，支持通配符
                "table": "student_name",
                # 表的主键配置
                "pks": ["id"],
                # kafka topic
                "topic": "student_name_logs"
            }
        ],
        # kafka 连接配置
        "kafkaConf": {
            "addrs": ["127.0.0.1:9092"]
        }
    }]
}
```