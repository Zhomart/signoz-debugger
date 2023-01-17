# How to debug Signoz

1. `docker-compose up -d`
2. Update `fake/log.json`
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
