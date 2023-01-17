# How to debug Signoz

https://github.com/SigNoz/signoz/issues/2058

Based on signoz 0.14.0 (branch main)

1. `docker-compose up -d`
2. (optional) Update `fake/log.json`
2. `docker-compose restart otel-collector`
2. `docker-compose logs -f otel-collector`
3. Check the logs.
    - If you're using `- type: stdout` in `filelog/custom`, it will log the output
4. Check clickhouse: http://localhost:8123/play
    - `show databases;`
    - `SHOW TABLES FROM signoz_logs`;
    - `describe signoz_logs.logs;`
    - `select * from signoz_logs.logs order by observed_timestamp desc limit 10;`
    - `select * from signoz_logs.logs where id = '<ID>'`
5. Open Signoz UI: http://localhost:3301/logs  
    - Change search dates
    - Search with id


## Useful docs

1. https://github.com/open-telemetry/opentelemetry-collector
  * Source code of Otel Collector. Read `docs/` and `receivers/` subfolders.
2. https://github.com/open-telemetry/opentelemetry-collector-contrib
  * Extensions to Otel Collector (syslog receiver is here). Read `receivers/` folder.
3. https://github.com/open-telemetry/opentelemetry-collector-contrib/blob/main/pkg/stanza/docs/operators
